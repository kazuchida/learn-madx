---
marp: true
---

# Twissパラメータとは

Twissパラメータ（ベータ関数）は、粒子加速器におけるビームの光学特性を記述する重要な物理量です。

---

# Twissパラメータの定義

ビームの包絡線は以下の式で表されます：

$$\gamma x^2 + 2\alpha x x' + \beta x'^2 = \epsilon$$

ここで：
- **β (ベータ関数)**: ビームサイズに関連
- **α (アルファ関数)**: ビームの発散性に関連  
- **γ (ガンマ関数)**: β, αから導出 (γ = (1+α²)/β)
- **ε (エミッタンス)**: ビームの位相空間体積

---

# 物理的意味

## ベータ関数 (β)
- ビームサイズ: σ = √(βε)
- 単位: [m]
- 小さいほど、ビームが細く絞られる

## アルファ関数 (α)
- ビームの収束/発散性を表す
- α > 0: 発散ビーム
- α < 0: 収束ビーム  
- α = 0: ビームウエスト

## 位相進行 (μ)
- dμ/ds = 1/β
- 格子の周期性を表す重要な量

---

# MAD-XでのTwiss計算

## 基本的な計算

```madx
! シーケンスの使用
USE, SEQUENCE=my_sequence;

! ビーム定義
BEAM, PARTICLE=PROTON, ENERGY=7000;

! Twiss計算
TWISS;
```

## 初期条件の指定

```madx
TWISS, BETX=10.0, BETY=10.0, ALFX=0.0, ALFY=0.0;
```

---

# 出力のカスタマイズ

## 出力列の選択

```madx
SELECT, FLAG=TWISS, COLUMN=NAME,S,BETX,BETY,ALFX,ALFY,MUX,MUY,DX,DY;
TWISS, FILE="twiss_output.tfs";
```

## 特定要素での出力

```madx
SELECT, FLAG=TWISS, CLASS=QUADRUPOLE;
TWISS, FILE="quad_twiss.tfs";
```

---

# 実践例：FODO格子

```madx
! 要素定義
QF: QUADRUPOLE, L=0.5, K1=1.2;
QD: QUADRUPOLE, L=0.5, K1=-1.2;
DRIFT: DRIFT, L=2.0;

! シーケンス定義
FODO: SEQUENCE, L=6.0;
    QF, AT=0.25;
    DRIFT, AT=1.25;
    QD, AT=3.25;  
    DRIFT, AT=4.25;
ENDSEQUENCE;

! Twiss計算
BEAM, PARTICLE=PROTON, ENERGY=1.0;
USE, SEQUENCE=FODO;
TWISS, BETX=10, BETY=10;
```

---

# 周期解の計算

```madx
! 周期境界条件でのTwiss計算
TWISS, CHROM, SUMMARY;

! チューン値の表示
VALUE, TABLE(SUMM,Q1), TABLE(SUMM,Q2);

! クロマティシティの表示  
VALUE, TABLE(SUMM,DQ1), TABLE(SUMM,DQ2);
```

---

# プロット作成

```madx
! データ選択
SELECT, FLAG=TWISS, COLUMN=NAME,S,BETX,BETY;
TWISS, FILE="plot_data.tfs";

! ベータ関数のプロット
PLOT, HAXIS=S, VAXIS=BETX,BETY, COLOUR=100;
```

---

# よく使用される出力パラメータ

| パラメータ | 説明 | 単位 |
|-----------|------|------|
| S | 位置座標 | m |
| BETX, BETY | 水平・垂直ベータ関数 | m |
| ALFX, ALFY | 水平・垂直アルファ関数 | - |
| MUX, MUY | 水平・垂直位相進行 | rad |
| DX, DY | 分散関数 | m |
| DPX, DPY | 分散の微分 | - |
| X, Y | 軌道座標 | m |
| PX, PY | 軌道角度 | rad |

---

# 応用：マッチング

Twissパラメータを使ったビーム光学のマッチング例：

```madx
MATCH, SEQUENCE=my_seq;
    VARY, NAME=KQF, STEP=0.0001;
    VARY, NAME=KQD, STEP=0.0001;
    CONSTRAINT, RANGE=#E, BETX=10.0, BETY=10.0;
    LMDIF, CALLS=1000, TOLERANCE=1.0E-21;
ENDMATCH;
```

---

# 参考資料

- [Twiss Parameters - CERN Accelerator School](https://cas.web.cern.ch/sites/cas.web.cern.ch/files/lectures/2016-senec/wiedemann-1.pdf)
- [MAD-X Twiss Module Documentation](http://madx.web.cern.ch/madx/doc/usrguide/twiss.html)
- [Beam Optics Fundamentals](https://inspirehep.net/literature/1469208)

