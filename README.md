# エンジニアのためのサウナ入門

技術書典21での頒布を目指す、サウナ入門書のRe:VIEW原稿リポジトリ。

## 本書のゴール

**エンジニアがサウナを、入り方から施設探し、作業場所として使うところまで自分で回せるようになる。**

サウナの入門書はすでにたくさんあります。本書が違うのは、エンジニアが書いているという一点です。

| 章 | 到達点 |
|---|---|
| 第1章 | なぜエンジニアにサウナなのかがわかる |
| 第2章 | 基本サイクルを組み、危ないラインを踏まずに入れる |
| 第3章 | サウナ施設を作業場所として評価・活用できる |
| 第4章 | サウナイキタイで自分に合う施設を検索条件から探せる |
| 第5章 | 関東の1軒目を決められる |
| 第6章 | 通い続けるコストを下げられる |
| 第7章 | 最初に買う1つを決められる |

## 対象読者

- サウナに興味があるエンジニア（未経験・初心者から、すでに通っている方まで）
- 作業できる場所としてサウナ施設を使ってみたい方
- 施設を人のおすすめではなく、自分の条件で探せるようになりたい方

## リポジトリ構成

| ファイル / ディレクトリ | 役割 |
|---|---|
| `catalog.yml` | 章立ての定義（章を追加したらここに登録する） |
| `config.yml` | Re:VIEWのメタデータ・出力設定 |
| `contents/*.re` | 本文（Re:VIEW記法） |
| `notes/` | 章立てメモ・タイトル案・作業計画 |
| `images/` | 図版・写真 |
| `sty/` | PDF出力用LaTeXスタイル（Re:VIEW upstream） |
| `style.css` | EPUB用CSS |
| `review-docs/` | Re:VIEW公式ドキュメント（記法リファレンス） |
| `.claude/skills/` | Claude Code用スキル（執筆方針、読みやすさレビュー、文体ガイド） |

## ビルド

PDFは [`vvakame/review:5.9`](https://hub.docker.com/r/vvakame/review) Dockerイメージで生成します。ローカルには `uplatex` がないため、PDFはDocker経由でのみ生成できます。

```sh
docker run --rm -v "$(pwd):/work" -w /work vvakame/review:5.9 review-pdfmaker config.yml
docker run --rm -v "$(pwd):/work" -w /work vvakame/review:5.9 review-epubmaker config.yml
```

EPUBだけならDockerなしでも生成できます。執筆中の確認はこちらで十分です。

```sh
bundle install
bundle exec review-epubmaker config.yml
```

mainへのpushおよびPRでは GitHub Actions が自動で `sauna-entry-book.pdf` / `sauna-entry-book.epub` をビルドし、artifactとして30日保管します。

## 執筆の進め方

1. `notes/outline.md` で構成を決める
2. `catalog.yml` に章を登録する
3. `contents/` に本文を書く（`book-writing-policy` スキルを参照）
4. 書き終えたら `readability-reviewer` スキルでレビューする

## 著者

[tadaken3](https://github.com/tadaken3)
