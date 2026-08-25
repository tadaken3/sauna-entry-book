# CLAUDE.md

技術同人誌『エンジニアのためのサウナ入門』のRe:VIEW原稿リポジトリ。技術書典21での頒布を目標とする。A5判・60〜80ページ想定。

本書のゴール「サウナ未経験のエンジニアが、今週末に1軒目へ行き、体を壊さずに2軒目へ行きたくなる」

## ディレクトリ構成

| パス | 役割 |
|---|---|
| `contents/` | 原稿本体（`.re` ファイル）。`config.yml` の `contentdir` で指定。 |
| `notes/` | 章立てアイデア・執筆メモ。ビルドには含まれない。 |
| `images/` | 原稿で参照する画像。 |
| `catalog.yml` | 章立ての唯一のソース（後述）。 |
| `config.yml` / `style.css` | Re:VIEWの設定。 |
| `sty/` | LaTeXスタイル一式。upstream純正は触らず、カスタマイズは `review-custom.sty` に追記する。 |
| `review-docs/` | Re:VIEW公式ドキュメント（参考資料）。記法で迷ったら `format.ja.md` を見る。 |
| `lib/` | Rakeタスク。 |

## ビルド

PDFは `vvakame/review:5.9` Dockerイメージで実行する（ローカルには `uplatex` がないため失敗する）。生成物はリポジトリルートに出力され、`.gitignore` 済み。

```sh
docker run --rm -v "$(pwd):/work" -w /work vvakame/review:5.9 review-pdfmaker config.yml
docker run --rm -v "$(pwd):/work" -w /work vvakame/review:5.9 review-epubmaker config.yml
```

EPUBと記法チェックだけならDockerなしでも動く。原稿を書いている途中の確認はこちらで足りる。

```sh
bundle install
bundle exec review-epubmaker config.yml        # EPUBを生成
bundle exec review-compile --target=latex chapter03.re   # 記法エラーの確認（引数は contents/ を含めないファイル名）
```

Gemfileの `review` のバージョンは、ビルドに使うDockerイメージと揃えてある。イメージを上げるときは両方同時に上げる。

## 章を追加・削除するとき

`catalog.yml` が章立ての唯一のソース。`contents/` 配下に `.re` ファイルを作っただけではビルドに含まれない。必ず `catalog.yml` の `PREDEF` / `CHAPS` / `APPENDIX` / `POSTDEF` のいずれかに登録する（パスは `contents/` を含めずファイル名のみ）。

構成そのものを変えるときは、先に `notes/outline.md` を更新してから `catalog.yml` と `contents/` を追従させる。

## 原稿を書く・レビューするとき

執筆タスクの段階に応じて2つのスキルを使い分ける。基準はスキル側に集約してあるので、ここで重複させない。

- **執筆前・執筆中** → `book-writing-policy` スキル（文体・安全記述の扱い・具体性・トーン）
- **執筆後** → `readability-reviewer` スキル（読点・助詞・図表・構成のレビュー）

## 健康・安全に関する記述の扱い

本書は医学書ではない。サウナの健康効果を断定して書かない（「自律神経が整います」「睡眠の質が上がります」は書かない）。一方で、危険を避けるための行動は曖昧にせず言い切る（「飲酒後は入らない」）。

持病・服薬・妊娠中の読者に対する「医師に相談する」の一文は、第4章に必ず残す。原稿を書き換えるときに消さない。

詳細な基準は `book-writing-policy` スキルの「方針1」を参照。

## スタイルのカスタマイズ

`sty/` 配下のうち、Re:VIEW upstream由来のファイル（`review-jsbook.cls`、`review-base.sty`、`review-style.sty`、`gentombow.sty` など）は触らない。これらを直接編集すると、upstream更新時のマージコストが上がるうえ、版面が壊れて入稿できないPDFになるリスクがある。

カスタマイズが必要な場合は `sty/review-custom.sty` に追記する。これは upstream が公式に用意している拡張口で、`sty/reviewmacro.sty` から自動的に読み込まれる。フォント・色・余白・見出し装飾など、追記ベースで足せるものは原則ここで対応する。

## 入稿まわり（未確定）

印刷所は未定。ねこのしっぽ・日光企画のように隠しノンブルが必要な印刷所を使う場合は、`config.yml` の `texdocumentclass` に `hiddenfolio=shippo` などを追加する（詳細は `sty/README.md`）。入稿先が決まるまでは追加しない。
