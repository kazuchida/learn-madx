# MAD-X 学習用レポジトリ

このレポジトリは、CERNで開発された加速器シミュレーションコード **MAD-X** の学習を目的としています。MAD-Xの基本文法、ユースケース、実践的な例題を通じて、独自の加速器設計に活用できる知識を習得できます。

## 📋 目次

1. [MAD-Xとは](#mad-xとは)
2. [セットアップ](#セットアップ)
3. [学習の進め方](#学習の進め方)
4. [ファイル構成](#ファイル構成)
5. [サンプルコード](#サンプルコード)
6. [参考資料](#参考資料)

## 🚀 MAD-Xとは

**MAD-X (Methodical Accelerator Design)** は、粒子加速器のビーム光学と格子設計のための無料シミュレーションコードです。

- **言語**: C/C++/Fortran で記述
- **特徴**: 単一粒子シミュレーション（PICシミュレーションではない）
- **ライセンス**: オープンソース
- **開発元**: CERN

## 🛠️ セットアップ

### MAD-Xのインストール

1. **公式サイトからダウンロード**:
   ```bash
   # macOS (Homebrew経由)
   brew install madx
   
   # Linux (Ubuntu/Debian)
   sudo apt-get install madx
   
   # ソースからコンパイル
   git clone https://github.com/MethodicalAcceleratorDesign/MAD-X.git
   cd MAD-X
   make
   ```

2. **動作確認**:
   ```bash
   madx --version
   ```

### このレポジトリの使用方法

```bash
git clone <このレポジトリのURL>
cd learn-madx
```

## 📚 学習の進め方

以下の順序で学習することを推奨します：

1. **学習計画** - [`tutorial_roadmap.md`](./tutorial_roadmap.md) - 個人の目標に応じた学習パス
2. **基礎概念** - [`lecture.md`](./lecture.md) - MAD-X概要とワークフロー  
3. **基本文法** - [`madx_basic_grammer.md`](./madx_basic_grammer.md) - 構文とコマンド
4. **Twissパラメータ** - [`twiss.md`](./twiss.md) - ビーム光学の基礎
5. **実習** - [`madx-sample-for-lecture/`](./madx-sample-for-lecture/)フォルダ - 段階的サンプル
6. **練習問題** - [`exercises.md`](./exercises.md) - 5段階の練習問題
7. **応用例** - [`madx-examples/`](./madx-examples/)フォルダ - CERNの実例
8. **サンプル集ガイド** - [`madx_examples_guide.md`](./madx_examples_guide.md) - CERN例の詳細説明

## 📁 ファイル構成

```
learn-madx/
├── README.md                    # このファイル
├── tutorial_roadmap.md          # 学習ロードマップ
├── exercises.md                 # 練習問題集
├── madx_examples_guide.md       # CERNサンプル集ガイド
├── lecture.md                   # MAD-X概要とワークフロー
├── madx_basic_grammer.md        # 基本文法の説明
├── twiss.md                     # Twissパラメータの説明
├── figures/                     # 図表類
│   └── diagrams.md             # 概念図とダイアグラム
├── madx-sample-for-lecture/     # 学習用サンプルコード
│   ├── beam.madx               # ビーム定義の例
│   ├── bend.madx               # 偏向磁石の例
│   ├── complete_example.madx   # 完全な学習例
│   ├── proton-linac.madx       # プロトン線形加速器の例
│   ├── sequence.madx           # シーケンス定義の例
│   ├── exercise1_solution.madx # 練習問題1解答
│   ├── exercise2_solution.madx # 練習問題2解答
│   ├── exercise3_solution.madx # 練習問題3解答
│   ├── exercise4_solution.madx # 練習問題4解答
│   └── exercise5_solution.madx # 練習問題5解答
└── madx-examples/              # CERNからの豊富なサンプル
    ├── aperture/               # アパーチャ関連
    ├── c6t/                    # チューン計算
    ├── dynap/                  # 動的アパーチャ
    ├── emit/                   # エミッタンス計算
    ├── error/                  # エラー解析
    ├── foot/                   # フットプリント解析
    ├── match/                  # マッチング例
    ├── twiss/                  # Twiss計算例
    └── ...                     # その他多数
```

## 🎯 サンプルコード

### 基本的な実行例

```bash
# ビーム定義の実行
madx < madx-sample-for-lecture/beam.madx

# Twiss計算の実行
madx < madx-examples/twiss/twiss_example.madx
```

### 基本的なMAD-Xスクリプトの構造

```madx
! 1. 要素の定義
QF: QUADRUPOLE, L=0.5, K1=1.2;
QD: QUADRUPOLE, L=0.5, K1=-1.2;

! 2. シーケンスの定義
CELL: SEQUENCE, L=10.0;
    QF, AT=2.5;
    QD, AT=7.5;
ENDSEQUENCE;

! 3. ビームの定義
BEAM, PARTICLE=PROTON, ENERGY=7000;

! 4. シーケンスの使用
USE, SEQUENCE=CELL;

! 5. Twiss計算
TWISS;
```

## 📖 参考資料

- [MAD-X 公式サイト](http://madx.web.cern.ch/madx/)
- [MAD-X GitHub リポジトリ](https://github.com/MethodicalAcceleratorDesign/MAD-X)
- [MAD-X Primer (PDF)](https://indico.cern.ch/event/509762/contributions/2450804/attachments/1487283/2338842/MAD-X-Primer.pdf)
- [MAD-X ユーザーガイド](http://madx.web.cern.ch/madx/doc/usrguide/usrguide.html)

## 🤝 貢献

このレポジトリの改善提案やバグ報告は、Issuesまたはプルリクエストでお願いします。

## 📄 ライセンス

このレポジトリの内容は教育目的で作成されています。MAD-X自体のライセンスについては、[公式リポジトリ](https://github.com/MethodicalAcceleratorDesign/MAD-X)をご確認ください。