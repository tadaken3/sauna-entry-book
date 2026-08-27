# images/

原稿から参照する画像を置く。

## ファイルの置き方

Re:VIEWは次の順で画像を探し、最初に見つかったものを使う（`review-docs/format.ja.md`）。

```
1. images/<builder>/<chapid>/<id>.<ext>
2. images/<builder>/<chapid>-<id>.<ext>
3. images/<builder>/<id>.<ext>
4. images/<chapid>/<id>.<ext>     ← 本書はこれを使う
5. images/<chapid>-<id>.<ext>
6. images/<id>.<ext>
```

本書は **4番目**の形式に統一する。章ごとにディレクトリを分ける。

```
images/chapter03/set-cycle.png     ← //image[set-cycle][...] から参照される
images/chapter08/moku.png
```

`<chapid>` は原稿のファイル名から `.re` を除いたもの。`chapter03.re` なら `chapter03`。

## 表紙

表紙は章の画像とは扱いが違う。`images/cover.jpg`（章ディレクトリなし、直下）に置き、
`config.yml` の `coverimage: cover.jpg` から参照する。これはEPUB（電子版）の表紙になる。

印刷版の表紙は入稿用の別データ（`cover-a5.ai` など）で作るため、本文PDFには入れない
（`config.yml` の `pdfmaker.coverimage` はコメントアウトのまま）。

現状は仮の表紙をCanvaで作成した段階。画像ファイルはまだリポジトリに入っていない。
`images/cover.jpg` を置いてから `config.yml` のコメントを外すこと。逆順にするとビルドが落ちる。

## 形式は PNG か JPEG

本書はPDFとEPUBの両方をビルドする。両方が扱える形式はPNGとJPEGのみ。

- **写真** → JPEG（`.jpg`）
- **図解・スクリーンショット** → PNG（`.png`）

| ビルダ | 対応する拡張子（優先順） |
|---|---|
| PDF（LaTeX） | .ai .eps .pdf .tif .tiff .png .bmp .jpg .jpeg .gif |
| EPUB（HTML） | .png .jpg .jpeg .gif .svg |

**SVGはPDF側で使えない**。図解をSVGで作った場合も、PNGに書き出してから置くこと。

迷ったらPNG。写真をPNGにするとファイルが無駄に大きくなるので、そこだけJPEGにする。

## 解像度

TODO: 印刷所が決まったら、その指定に合わせて確定する。

一般的な同人誌の入稿では、原寸で350dpiが目安。A5判（148×210mm）の版面幅に対して全幅で使う画像なら、およそ1500px以上あれば足りる計算になる。

画面のスクリーンショットは、Retinaディスプレイなら等倍でも十分な密度がある。縮小はしない。

## 撮影・掲載のルール

- **浴室内・脱衣所での撮影は、どの施設でも禁止**。例外はない
- 施設の外観・館内の共用部・食事は、施設のルールを確認したうえで撮る
- サービスの画面キャプチャは、掲載可否を運営に確認する
- グッズは私物を自分で撮る。メーカーの商品画像を転載しない

## 記法

```
//image[set-cycle][1セットの流れ]{
図が表示できない環境向けの代替テキストをここに書く
//}
```

本文から参照するときは `@<img>{set-cycle}`。`//image` と `@<img>` でつづりが違う。

**ファイルを置く前に `//image` を書くとビルドが落ちる**。画像を用意してから記法を書くこと。原稿には `#@#` コメントで挿入位置と記法を用意してある。
