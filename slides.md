---
theme: seriph
background: https://source.unsplash.com/collection/94734566/1920x1080
class: text-center
highlighter: shiki
lineNumbers: true
info: |
  ## Issueテンプレートは古い、これからはIssue Formだ

  これは[【現地/オンライン配信】GitHub dockyardコミュニティ 竣工イベント！](https://github-dockyard.connpass.com/event/289714/)でLT登壇したスライドです。
drawings:
  persist: false
transition: slide-left
title: Issueテンプレートは古い、これからはIssue Formだ
---

# Issueテンプレートは古い<br>これからはIssue Formだ

[GitHub dockyardコミュニティ 竣工イベント！](https://github-dockyard.connpass.com/event/289714/)@[コワーキングスペース茅場町 Co-Edo](https://blog.coworking.tokyo.jp/p/access.html)


2023/08/05

Yuhei FUJITA

---
layout: two-cols
---


![](https://github.com/YuheiFUJITA.png)

::right::
# Who am I ?

|  |  |
| --- | --- |
| Name | Yuhei FUJITA |
| Blog | 個人: https://fujita.dev<br>Zenn: https://zenn.dev/yuhei_fujita |
| SNS | X'sするやつ: [@Yuhei_FUJITA](https://twitter.com/Yuhei_FUJITA)<br>Instagram: [yuhei_fujita.film](https://www.instagram.com/yuhei_fujita.film/)|
| 趣味 | 自転車 / キャンプ / フィルムカメラ |
| Tech | Vue.js / TypeScript |
| Community | [Vue Fes](https://vuefes.jp/2023/) / [PWA Night](https://pwanight.connpass.com/) / [VS Code Meetup](https://vscode.connpass.com/) |

---

# Vue Fes Japan 2023 スポンサー募集中

[![](/vue-fes.png)](https://vuefes.jp/2023/#sponsors)

---
layout: statement
---

# Issue Template使ってますか？

---
layout: statement
---

# 🙆 or 🙅

---
layout: statement
---

# たぶん🙆が多いと思う

---

# Issue Templateの復習

<div class="grid grid-cols-2 gap-4">
<div>

## .github/ISSUE_TEMPLATE

テンプレートファイルを作成する。

```txt {3-6}
/
├── README.md
├── .github
│   ├── ISSUE_TEMPLATE
│   │   ├── bug-report.md
│   │   └── feature-request.md
│   └── workflows
│       └── deploy.yml
├── netlify.toml
├── package-lock.json
├── package.json
├── slides copy.md
├── slides.md
└── vercel.json
```

</div>
<div>

## template-name.md

IssueのテンプレートをMarkdownで書く。

```md
---
name: Bug Report
description: 不具合の報告
title: '[Bug] '
labels: [bug]
assignees:
  - YuheiFUJITA
---
<!--
不具合報告時は以下のテンプレートに沿って記載してください。
各項目は必ず記載してください。
-->
## 概要
<!--不具合の具体的な内容を記載してください。（この行は消してください）-->
## 環境
<!--不具合が発生した環境を選んでください。（この行は消してください）-->
- [ ] Google Chrome
- [ ] Safari
- [ ] Firefox
```

</div>
</div>

---
layout: statement
---

# しかし現実は非情なり

---
layout: statement
---

# そう、誰もテンプレートを<br>守らないのである

---
layout: statement
---

# 👹

---
layout: statement
---

# Issue Formを使おう

---

# Issue Formの使い方

<div class="grid grid-cols-2 gap-4">
<div>

## .github/ISSUE_TEMPLATE

**YAMLで**テンプレートファイルを作成する。

```diff {3-8}
  /
  ├── README.md
  ├── .github
  │   ├── ISSUE_TEMPLATE
- │   │   ├── bug-report.md
+ │   │   ├── bug-report.yml
- │   │   └── feature-request.md
+ │   │   └── feature-request.yml
  │   └── workflows
  │       └── deploy.yml
  ├── netlify.toml
  ├── package-lock.json
  ├── package.json
  ├── slides copy.md
  ├── slides.md
  └── vercel.json
```

</div>
<div>

## template-name.yml

IssueのフォームをYAMLで定義する。

```yml {all|1-6|7-}
name: Bug Report
description: 不具合の報告
title: '[Bug] '
labels: [bug]
assignees:
  - YuheiFUJITA
body:
  - type: markdown
    attributes:
      label: 概要
      description: 不具合の具体的な内容を記載してください。
    validations:
      required: true
  - type: checkboxes
    attributes:
      label: 環境
      description: 不具合が発生した環境を選んでください。
      choices:
        - Google Chrome
        - Safari
        - Firefox
    validations:
      required: true
```

</div>
</div>

---

# 使える入力形式

<div class="grid grid-cols-2 gap-4">
<div>

```yml
- type: textarea
  attributes:
    label: Operating System
    description: What operating system are you using?
    placeholder: Example: macOS Big Sur
    value: operating system
  validations:
    required: true
- type: dropdown
  attributes:
    label: Version
    description: What version of our software are you running?
    multiple: false
    options:
      - 1.0.2 (Default)
      - 1.0.3 (Edge)
  validations:
    required: true
- type: checkboxes
  attributes:
    label: Code of Conduct
    description: The Code of Conduct helps create a safe space for everyone. We require
      that everyone agrees to it.
    options:
      - label: I agree to follow this project's [Code of Conduct](link/to/coc)
        required: true
- type: markdown
  attributes:
    value: "Thanks for completing our form!"
```

</div>
<div>

<v-clicks depth="1">

- markdown
  - ユーザーに表示するためのテキスト（説明文など）
  - Issueには送信されない
- textarea
  - GitHubのMarkdown記法で記述できる
  - 画像も貼れる
- input
  - 単一行のテキスト入力
- dropdown
  - ドロップダウンメニュー
- checkboxes
  - チェックボックス
  - 複数選択可能

</v-clicks>

</div>
</div>
---

# Issue Formのメリット・デメリット

<div class="grid grid-cols-2 gap-4">
<div>

## メリット

<v-clicks depth="1">

- フォーマットを強制できる
  - フォームになるので勝手に項目を変更されない
- 入力を必須にできる
  - `validations.required: true` をつけると入力が必須になる
- query stringでデフォルト値を設定できる
  - `id=value` とすると `id` のデフォルト値が `value` になる

</v-clicks>

</div>
<div>

## デメリット

<v-clicks depth="1">

- Issue FormがあるとMarkdownのテンプレートが出てこない？
  - `New issue` のリストにIssue Formしか出ないから併用できない？
  - queryで指定すればいける
- まだBeta機能
  - 今後変更される可能性あり
- `required: true` はPublic Repositoryのみ
  - Private Repositoryではすべて `required: false` になる（なんで？？？）

</v-clicks>

</div>
</div>

---
layout: statement
---

# [DEMO](https://github.com/YuheiFUJITA/sample-issue-form/issues/new/choose)

---
layout: end
---



# Thank you !

- [YuheiFUJITA/sample\-issue\-form](https://github.com/YuheiFUJITA/sample-issue-form)
- [Syntax for issue forms \- GitHub Docs](https://docs.github.com/en/communities/using-templates-to-encourage-useful-issues-and-pull-requests/syntax-for-issue-forms)
- [Syntax for GitHub's form schema \- GitHub Docs](https://docs.github.com/en/communities/using-templates-to-encourage-useful-issues-and-pull-requests/syntax-for-githubs-form-schema)

