# MAD-X学習ロードマップ

このドキュメントは、MAD-Xを効率的に学習するための推奨パスを示します。

## 🎯 学習目標別コース

### 初心者コース（1-2週間）
MAD-Xを初めて使う方向け

1. **基礎理解** (1-2日)
   - [`lecture.md`](./lecture.md) - MAD-X概要
   - [`figures/diagrams.md`](./figures/diagrams.md) - 基本概念図

2. **文法習得** (2-3日)
   - [`madx_basic_grammer.md`](./madx_basic_grammer.md) - 基本文法
   - [`madx-sample-for-lecture/beam.madx`](./madx-sample-for-lecture/beam.madx) - ビーム定義

3. **実践演習** (3-4日)
   - [`madx-sample-for-lecture/sequence.madx`](./madx-sample-for-lecture/sequence.madx) - シーケンス定義
   - [`madx-sample-for-lecture/complete_example.madx`](./madx-sample-for-lecture/complete_example.madx) - 完全例

4. **基礎演習** (2-3日)
   - [`exercises.md`](./exercises.md) - 練習問題1-2

### 中級者コース（2-3週間）
基本操作ができる方向け

1. **Twiss解析** (3-4日)
   - [`twiss.md`](./twiss.md) - Twissパラメータ詳細
   - [`madx-examples/twiss/`](./madx-examples/twiss/) - 実例

2. **マッチング技術** (4-5日)
   - [`madx-examples/match/`](./madx-examples/match/) - マッチング例
   - [`exercises.md`](./exercises.md) - 練習問題3-4

3. **エラー解析** (3-4日)
   - [`madx-examples/error/`](./madx-examples/error/) - エラー例
   - [`exercises.md`](./exercises.md) - 練習問題5

### 上級者コース（3-4週間）
実際の加速器設計を行う方向け

1. **高度な追跡** (1週間)
   - [`madx-examples/dynap/`](./madx-examples/dynap/) - 動的アパーチャ
   - [`madx-examples/foot/`](./madx-examples/foot/) - フットプリント

2. **実機シミュレーション** (2-3週間)
   - [`madx-examples/`](./madx-examples/) 内の実機例
   - LHC, RHIC等の大型加速器例

## 📚 学習リソース分類

### 理論・概念
- [`lecture.md`](./lecture.md) - MAD-X概要とワークフロー
- [`twiss.md`](./twiss.md) - Twissパラメータ理論
- [`figures/diagrams.md`](./figures/diagrams.md) - 視覚的説明

### 文法・構文
- [`madx_basic_grammer.md`](./madx_basic_grammer.md) - 基本文法完全版
- [`madx-sample-for-lecture/`](./madx-sample-for-lecture/) - 基本例

### 実践・応用
- [`exercises.md`](./exercises.md) - 段階別練習問題
- [`madx-examples/`](./madx-examples/) - CERNからの豊富な実例

## 🛠️ 実習環境

### 必要ソフトウェア
```bash
# MAD-X本体
brew install madx  # macOS
apt install madx   # Linux

# プロット用（オプション）
pip install matplotlib numpy
apt install gnuplot
```

### 推奨エディタ設定
- VS Code + MAD-X syntax highlighting
- Vim/Emacs + カスタムハイライト

## 📈 習熟度チェックリスト

### 初級（✓でマーク）
- [ ] MAD-Xの基本概念を説明できる
- [ ] 簡単な要素定義ができる
- [ ] シーケンスを作成できる  
- [ ] Twiss計算を実行できる
- [ ] 基本的なプロットが作れる

### 中級
- [ ] マッチング機能を使用できる
- [ ] エラー定義と解析ができる
- [ ] 複雑なシーケンスを構築できる
- [ ] 粒子追跡計算ができる
- [ ] 結果を適切に解釈できる

### 上級
- [ ] 実機レベルの格子設計ができる
- [ ] 高度な最適化技術を使える
- [ ] 動的効果を考慮できる
- [ ] オリジナルの解析スクリプトが書ける
- [ ] 他の加速器コードと連携できる

## 💡 学習のコツ

1. **段階的学習**: 基礎から順番に進む
2. **実習重視**: 理論と実践を並行して行う
3. **エラー活用**: エラーメッセージから学ぶ
4. **コミュニティ活用**: CERN MAD-Xフォーラムを利用
5. **継続的実践**: 定期的にコードを書く

## 🔗 参考リンク

### 公式ドキュメント
- [MAD-X ユーザーガイド](http://madx.web.cern.ch/madx/doc/usrguide/usrguide.html)
- [MAD-X Primer](https://indico.cern.ch/event/509762/contributions/2450804/attachments/1487283/2338842/MAD-X-Primer.pdf)

### コミュニティ
- [MAD-X GitHub](https://github.com/MethodicalAcceleratorDesign/MAD-X)
- [CERN フォーラム](https://mad-forum.cern.ch/)

### 論文・書籍
- 加速器物理学の基礎書
- ビーム光学関連論文
