# エンジニアのためのサウナ入門 ── 週末の90分で整える人になる

技術書典21での頒布を目指す、サウナ入門書のRe:VIEW原稿リポジトリ。

> タイトルは暫定です。候補と判断基準は `notes/title-ideas.md` にまとめています。

## 本書のゴール

**サウナ未経験のエンジニアが、今週末に1軒目へ行き、体を壊さずに2軒目へ行きたくなる。**

「ととのう」ことを目的にした本ではありません。初回で失敗せず、危ないラインを踏まずに、自分のペースを見つけるための手順書です。

| 章 | 到達点 |
|---|---|
| 第1章 | サウナのなにが良いのかがわかる |
| 第2章 | 1軒目を選び、持ち物を揃えて当日の動線がわかる |
| 第3章 | サウナ室・水風呂・外気浴の基本サイクルを組める |
| 第4章 | 体調を崩さないラインを引ける |
| 第5章 | 施設の違いがわかり、次の一軒を選べる |
| 第6章 | 続ける仕組みを作れる |

## 対象読者

- サウナに入ったことがない、または数回しか入ったことがない方
- 「ととのう」という言葉は知っているが、実感がない方
- 温浴施設のマナーがわからず、入る前から不安な方

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
