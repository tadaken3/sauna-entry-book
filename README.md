# エンジニアのためのサウナ入門

技術書典21での頒布を目指す、サウナ入門書のRe:VIEW原稿リポジトリ。

## 本書のゴール

**最後のページを閉じた読者が「よし、サウナ行ってみよう。」と思うこと。**

根底にあるメッセージは「サウナに入ると、人生すべてうまくいく。」です。文字どおり何もかも解決するという意味ではありません。ストレスを感じたときに、気軽に日常から離れてリフレッシュできる手段を持っている。それだけで少し前向きになれる、という話です。

本書が伝えたいのは「サウナへの愛 × サウナの楽しみ方 × 安全に楽しむための知識」の3つです。

| 章 | 到達点 |
|---|---|
| 第1章 | サウナに行ってみたくなる |
| 第2章 | 安全に楽しむラインを引ける |
| 第3章 | 身体ひとつで1軒目に行ける |
| 第4章 | サウナイキタイで次の一軒を自分で探せる |
| 第5章 | 1軒目を決められる |
| 第6章 | サウナ施設を作業場所として使える |
| 第7章 | 通い続けるコストを下げられる |
| 第8章 | 最初に買う1つを決められる |

## 対象読者

- サウナ初心者、これからサウナを趣味にしてみたい方
- 「ととのう」は聞いたことがあるが、実感がない方
- ストレス解消の手段を探している方

## 執筆方針

著者自身のストーリー（宙に浮くような感覚 → ハマる → 体調を崩す → 学ぶ → サウナ・スパ健康アドバイザー取得 → 初心者へ伝える）を本書の背骨としています。

体験談と客観的事実は文中で見分けがつく形に書き分け、根拠を確認できない健康効果は書きません。詳細は `.claude/skills/book-writing-policy/SKILL.md` を参照してください。

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

### Claude Code のワークフロー（任意）

`claude.yml`（`@claude` メンションでの起動）と `claude-code-review.yml`（PRの自動レビュー）も用意していますが、動かすには `CLAUDE_CODE_OAUTH_TOKEN` のシークレット登録が必要です。

リポジトリの Settings → Secrets and variables → Actions から追加してください。トークンは Claude Code CLI で `claude setup-token` を実行すると取得できます。

**未設定のあいだ、この2つのワークフローは自動でスキップされます**（CIは失敗しません）。

## 執筆の進め方

1. `notes/outline.md` で構成を決める
2. `catalog.yml` に章を登録する
3. `contents/` に本文を書く（`book-writing-policy` スキルを参照）
4. 書き終えたら `readability-reviewer` スキルでレビューする

## 著者

[tadaken3](https://github.com/tadaken3)
