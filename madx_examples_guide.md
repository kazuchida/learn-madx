# CERN MAD-X サンプル集ガイド

このドキュメントは、`madx-examples/`フォルダに含まれるCERN公式サンプルの使用方法と学習順序を説明します。

## 📁 サンプル分類

### 🟢 初心者向け（基本機能）
学習開始時に理解すべき基本的な機能

#### `twiss/` - Twiss計算
- **目的**: 線形光学パラメータの計算
- **含まれる例**:
  - 基本的なTwiss計算
  - 周期境界条件
  - カスタム出力
- **学習ポイント**: ベータ関数、分散関数、チューン

#### `aperture/` - アパーチャ
- **目的**: ビームパイプのサイズ制限
- **含まれる例**:
  - `lhccell.madx` - LHC格子のアパーチャ
  - アパーチャ制限の可視化
- **学習ポイント**: 物理アパーチャ vs 動的アパーチャ

### 🟡 中級者向け（応用機能）

#### `match/` - マッチング
- **目的**: 格子パラメータの最適化
- **サブフォルダ**:
  - `global-tune/` - グローバルチューン調整
  - `global-equal-tune/` - 等チューン設定
  - `lhc-cell/` - LHC格子マッチング
  - `5cell/` - 5セル格子の例
- **学習ポイント**: 制約条件設定、最適化アルゴリズム

#### `error/` - エラー解析
- **目的**: 磁石誤差とアライメント誤差の影響
- **含まれる例**:
  - `example1.mad` - 基本的なエラー定義
  - `example2.mad` - 統計的エラー解析
  - `example3.mad` - 軌道補正
- **学習ポイント**: 誤差設定、統計解析、補正

#### `emit/` - エミッタンス
- **目的**: ビームエミッタンスの計算と制御
- **サブフォルダ**:
  - `ALBA/` - ALBA光源の例
  - `LEP/` - LEP加速器の例
- **学習ポイント**: 放射減衰、平衡エミッタンス

### 🔴 上級者向け（専門機能）

#### `dynap/` - 動的アパーチャ
- **目的**: 非線形効果による長期安定性
- **サブフォルダ**:
  - `FODO/` - FODO格子の動的アパーチャ
  - `LHC_footprint/` - LHCチューンフットプリント
- **学習ポイント**: 非線形共鳴、カオス現象

#### `foot/` - フットプリント解析
- **目的**: チューンスプレッドと共鳴線
- **含まれるツール**:
  - `footprint.mad` - メインスクリプト
  - `foot.c` - C言語解析ツール
  - `dynaptune` - 動的チューン計算
- **学習ポイント**: チューン図、共鳴駆動項

#### `ibs/` - ビーム内散乱
- **目的**: クーロン散乱によるエミッタンス成長
- **サブフォルダ**:
  - `LhcProtonRun/` - LHC陽子運転
  - `LhcTopEnergy/` - LHC最高エネルギー
  - `ClicDampingRing/` - CLIC制動リング
- **学習ポイント**: 散乱率計算、エミッタンス進化

#### `touschek/` - Touschek効果
- **目的**: ビーム内散乱によるビーム寿命
- **学習ポイント**: 寿命計算、散乱断面積

## 🎯 学習順序推奨

### ステップ1: 基本機能習得
1. `twiss/` - 基本計算を理解
2. `aperture/` - 物理制限を学ぶ

### ステップ2: 設計技術習得  
3. `match/global-tune/` - チューン調整
4. `match/lhc-cell/` - 実用的マッチング
5. `error/example1.mad` - 基本誤差解析

### ステップ3: 高度な解析
6. `emit/ALBA/` - エミッタンス計算
7. `dynap/FODO/` - 動的アパーチャ入門
8. `foot/` - フットプリント解析

### ステップ4: 専門応用
9. `ibs/` - ビーム物理現象
10. `touschek/` - 寿命計算

## 💻 実行方法

### 基本的な実行
```bash
cd madx-examples/twiss
madx < example.madx
```

### 出力ファイルの確認
```bash
# Twiss出力
cat twiss.out
head -20 twiss.tfs

# プロットファイル
ls *.ps *.png
```

### 結果の解析
```bash
# GNUplotでの可視化
gnuplot plot_script.gnu

# Pythonでの解析
python analyze_results.py
```

## 📊 各例の詳細説明

### `match/global-tune/`
```madx
! チューン値を指定値に調整
MATCH;
    VARY, NAME=kqf, STEP=0.001;
    VARY, NAME=kqd, STEP=0.001;
    GLOBAL, Q1=6.28, Q2=6.31;  ! 目標チューン
    LMDIF, CALLS=1000;
ENDMATCH;
```

### `error/example1.mad`
```madx
! アライメントエラーの設定
SELECT, FLAG=ERROR, CLASS=QUADRUPOLE;
EALIGN, DX:=GAUSS()*0.0001, DY:=GAUSS()*0.0001;
```

### `dynap/FODO/`
```madx
! 動的アパーチャの計算
DYNAP, FASTUNE=false, TURNS=1024, 
       LYAPUNOV=true, MAXAPER={0.1,0.1};
```

## 🔧 カスタマイズのヒント

### パラメータ調整
- エネルギー、粒子種の変更
- 格子長、磁石強度の調整
- 計算精度、ターン数の設定

### 出力カスタマイズ
- プロット範囲の変更
- 出力列の選択
- ファイル形式の指定

### 解析スクリプト作成
- 結果の自動処理
- パラメータスキャン
- 統計解析の追加

## 📚 参考資料

### CERN公式
- [MAD-X Examples Documentation](http://madx.web.cern.ch/madx/doc/usrguide/introduction.html)
- [CERN Accelerator School](https://cas.web.cern.ch/)

### 論文・書籍
- "Handbook of Accelerator Physics and Engineering" - World Scientific
- "An Introduction to the Physics of High Energy Accelerators" - Wiley

### オンラインリソース
- [MAD-X Forum](https://mad-forum.cern.ch/)
- [Accelerator Physics Stack Exchange](https://physics.stackexchange.com/)
