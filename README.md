# My Codex Skills

Codex で利用する個人用スキルをまとめるためのリポジトリです。

現時点では、既存の、部分的に完成しているソフトウェアプロジェクトを保守するための `project-maintenance` スキルを収録しています。このスキルは、広範な再設計や不要なリファクタリングを避けながら、現在のコードを一次情報として読み取り、仕様・ADR・テスト・実装を最小差分でそろえるためのワークフローを提供します。

## 含まれるもの

### `project-maintenance`

既存プロジェクトの保守を、ドキュメント確認、仕様更新、ADR作成、最小差分の実装、テスト確認の流れで進めるためのスキルです。

- `project-maintenance/SKILL.md`: スキル本体
- `project-maintenance/references/documentation-rules.md`: ドキュメント作成・更新時の判断ルール
- `project-maintenance/references/spec-template.md`: 仕様書の分割基準とテンプレート
- `project-maintenance/references/adr-template.md`: ADR の作成基準とテンプレート
- `project-maintenance/agents/openai.yaml`: エージェント向け表示名・説明・既定プロンプト

## 使い方

各スキルは、Codex から明示的に呼び出して使います。

`project-maintenance` の例:

```text
$project-maintenance bootstrap
$project-maintenance inspect
$project-maintenance docs-check
$project-maintenance change "<変更内容>"
```

各モードの用途は次のとおりです。

- `bootstrap`: 既存プロジェクトを読み取り、保守用ドキュメントを作成する
- `inspect`: 読み取り専用で、構成・リスク・不足しているドキュメントを確認する
- `docs-check`: コード、仕様、ADR、テストの不一致や不足を確認する
- `change "<変更内容>"`: 仕様やADRを必要に応じて更新してから、最小差分で実装する

## 基本方針

- 現在のコードを、観測可能な一次情報として扱う
- コードとドキュメントが矛盾する場合は、片方を勝手に正とせず矛盾として報告する
- 既存の動作を、明示された変更なしに壊さない
- 広範な再設計、無関係な整理、不要な依存関係追加を避ける
- 実装前に、変更分類・影響範囲・リスク・テスト方針を明らかにする
- テスト追加は、変更された振る舞いと近い回帰リスクに絞る

## ディレクトリ構成

```text
.
├── LICENSE
├── README.md
└── project-maintenance/
    ├── SKILL.md
    ├── agents/
    │   └── openai.yaml
    └── references/
        ├── adr-template.md
        ├── documentation-rules.md
        └── spec-template.md
```

## メンテナンス時の注意

スキル本体を変更する場合は、各スキルの `SKILL.md` と `references/` 配下のルールが矛盾しないようにしてください。

`project-maintenance` のテンプレートを変更する場合は、既存プロジェクトへ生成される `docs/overview.md`、`docs/decisions.md`、`docs/specs/`、`docs/adr/` の運用に影響が出る可能性があります。変更理由と影響範囲を確認してから更新することを推奨します。

## ライセンス

このリポジトリは `LICENSE` に記載された CC0 1.0 Universal の条件で提供されています。
