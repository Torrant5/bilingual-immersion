# Bilingual Immersion Agent Skill

A portable Agent Skill that turns everyday conversations with an AI coding agent into lightweight reading practice. It mixes complete sentences in a target language into direct conversational replies while keeping task accuracy, safety, generated artifacts, automation output, and code text intact.

Designed for Codex and Claude Code using the open Agent Skills format.

## Features

- Uses sentence-level immersion instead of swapping isolated words.
- Defaults to 20% of eligible sentences and beginner-level English, with ratio and difficulty controlled separately.
- Supports a user-selected target language.
- Chooses easy, context-inferable sentences first instead of selecting sentences randomly.
- Leaves every requested artifact or copy-ready deliverable unchanged, including documents, email, posts, reports, prompts, translations, and UI copy.
- Leaves code text, scheduled or automated output, commands, quotes, logs, errors, file contents, and safety-critical wording unchanged.
- Explains the latest target-language sentence in the user's main language when asked, then lowers difficulty and reduces the mix.
- Automatically uses less immersion when a reply is short, risky, or precision-sensitive.

## Installation

Clone the repository:

```bash
git clone \
  https://github.com/Torrant5/bilingual-immersion.git
```

Install for Codex (user-wide):

```bash
mkdir -p \
  ~/.agents/skills
cp -R \
  bilingual-immersion/skills/bilingual-immersion \
  ~/.agents/skills/
```

Install for Claude Code (user-wide):

```bash
mkdir -p \
  "$HOME/.claude/skills"
cp -R \
  bilingual-immersion/skills/bilingual-immersion \
  "$HOME/.claude/skills/"
```

For another Agent Skills-compatible tool, copy `skills/bilingual-immersion/` into that tool's skills directory. Restart or reload the agent if it does not discover new skills automatically.

Installing the skill makes it available; it does not guarantee activation on every unrelated prompt. Invoke it explicitly at the start of a conversation. For optional always-on use, add a short instruction such as the following to your host's persistent guidance (`~/.codex/AGENTS.md` for Codex or `~/.claude/CLAUDE.md` for Claude Code):

```text
Apply the bilingual-immersion skill to direct conversational replies with 20% beginner-level English unless I change the ratio, difficulty, or turn it off. Do not apply it to generated artifacts, copy-ready content, scheduled or automated output, tool payloads, or any text inside code.
```

## Usage

Invoke the skill and optionally specify a target language and ratio:

```text
Use $bilingual-immersion with 20% English.
```

You can adjust it during the conversation:

```text
Increase the English mix to 40%.
Switch the target language to Spanish at 20%.
Make the English easier.
Use intermediate English.
I didn't understand the last English sentence.
Turn the language mix off.
```

The percentage applies to eligible sentences, so the actual mix may be lower when clarity or safety requires it. Difficulty is independent from that percentage: the skill starts at the easiest end of beginner, gradually uses more of the current level's range, and only moves to the next level when you ask for it or show understanding across separate turns.

## Limitations

- This is prompt-based behavior, so ratios are approximate and model-dependent.
- Difficulty adaptation is prompt-based too, so it is conservative rather than a precise proficiency test.
- Only direct conversational prose is eligible. Generated artifacts, scheduled or automated output, and text inside code stay in their required language.
- It generates mixed replies directly; it does not rewrite existing pages or past messages.
- It has no click-to-translate interface. Ask for the source-language meaning instead.
- It stores no settings or conversation data and makes no network requests by itself.

## Inspiration

Conceptual inspiration: [Mazelingo](https://mazelingo-web.pages.dev/), an independent service that mixes languages at sentence boundaries for reading practice. This project independently applies that high-level idea to direct AI-agent conversations. It is not affiliated with or endorsed by Mazelingo or Finer, and does not use Mazelingo's code, assets, copy, or proprietary implementation.

---

日常的なAIコーディングエージェントとの会話を、軽い読解練習に変えるポータブルな Agent Skill です。作業の正確さ、安全性、生成物、自動処理の出力、コード内の文章を保ちながら、直接会話の返答だけを対象言語の完全な文に置き換えます。

オープンな Agent Skills 形式を使用し、CodexとClaude Code向けに設計しています。

## 特徴

- 単語だけを差し替えず、文単位でイマージョンを行います。
- 対象となる文の20%と beginner レベルを既定値とし、割合と難易度を別々に変更できます。
- 対象言語をユーザーが指定できます。
- ランダムに文を選ばず、まずは短く、具体的で、前後から意味を推測しやすい文を選びます。
- 文書、メール、投稿、レポート、プロンプト、翻訳、UI文言など、依頼された生成物やそのまま使う文章は変更しません。
- コード内の文章、定時実行や自動化の出力、コマンド、引用、ログ、エラー、ファイル内容、重要な安全確認は変更しません。
- 分からないと伝えると、直近の対象言語の文を母語で説明し、その後の難易度と割合を下げます。
- 短い返答、高リスクな作業、厳密さが必要な場面では自動的に割合を下げます。

## インストール

リポジトリを取得します。

```bash
git clone \
  https://github.com/Torrant5/bilingual-immersion.git
```

Codexへユーザー共通でインストールします。

```bash
mkdir -p \
  ~/.agents/skills
cp -R \
  bilingual-immersion/skills/bilingual-immersion \
  ~/.agents/skills/
```

Claude Codeへユーザー共通でインストールします。

```bash
mkdir -p \
  "$HOME/.claude/skills"
cp -R \
  bilingual-immersion/skills/bilingual-immersion \
  "$HOME/.claude/skills/"
```

その他の Agent Skills 対応ツールでは、`skills/bilingual-immersion/` をそのツールのスキル用ディレクトリへコピーしてください。スキルが自動検出されない場合は、エージェントを再起動または再読み込みします。

インストールだけでは、無関係なすべての依頼で必ず自動起動するわけではありません。会話の開始時に明示的に呼び出してください。常時利用したい場合は、ホストの永続指示（Codexは `~/.codex/AGENTS.md`、Claude Codeは `~/.claude/CLAUDE.md`）へ、次のような短い指示を任意で追加できます。

```text
直接会話の返答には bilingual-immersion スキルを適用し、変更またはOFFの指定がない限り beginner レベルの英語を20%混ぜる。生成物、そのまま使う文章、定時実行や自動化の出力、ツールへ渡す内容、コード内の文章には適用しない。
```

## 使い方

スキルを呼び出し、必要なら対象言語と割合を指定します。

```text
$bilingual-immersion を使って、英語を20%混ぜて。
```

会話の途中でも変更できます。

```text
英語を40%に上げて。
対象言語をスペイン語、割合を20%に変更して。
英語をもっと簡単にして。
英語の難易度を intermediate にして。
さっきの英語の文が分からなかった。
言語ミックスをオフにして。
```

割合は「変換可能な文」を基準にするため、明瞭さや安全性を優先する場面では実際の割合が低くなることがあります。難易度は割合とは別に扱われ、初級の中でも最も簡単な文から始めて、同じ段階の範囲を少しずつ広げます。次の段階へ進むのは、ユーザーが求めた場合か、別々のターンで理解できていることが確認できた場合だけです。

## 制限事項

- プロンプトによる挙動のため、割合は概算であり、モデルによって差が出ます。
- 難易度の調整もプロンプトによる挙動のため、厳密な語学力判定ではなく保守的な目安です。
- 対象は直接会話の説明文だけです。生成物、定時実行や自動化の出力、コード内の文章は必要な言語のまま維持します。
- 既存ページや過去の発言を後処理せず、混在した返答を直接生成します。
- クリックによる言語切替はありません。分からない文は母語での説明を依頼してください。
- スキル自体は設定や会話データを保存せず、ネットワーク通信も追加しません。

## 着想

着想: [Mazelingo](https://mazelingo-web.pages.dev/) の、文単位で二言語を混ぜる読解体験。本プロジェクトは、その高水準のアイデアをAIエージェントとの直接会話向けに独自実装した非公式プロジェクトです。Mazelingoおよび株式会社Finerとは提携・承認関係になく、同サービスのコード、素材、文言、非公開実装は使用していません。

## License / ライセンス

[MIT](LICENSE)
