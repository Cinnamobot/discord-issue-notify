# discord-issue-notify

GitHub の Issue 作成・クローズ・削除を Discord に通知する Reusable Workflow です。

## 通知内容

- 変更された Issue の情報（タイトル・番号・リンク）
- 現在オープン中の Issue 一覧

## 使い方

### 1. Secretsの登録

通知したいリポジトリの **Settings → Secrets and variables → Actions** から以下を登録します。

| Secret名 | 内容 |
|---|---|
| `DISCORD_WEBHOOK_URL` | Discord の Webhook URL |

> Discord Webhook URL の取得方法：サーバー設定 → 連携サービス → ウェブフック → 新しいウェブフック

### 2. ワークフローファイルの追加

通知したいリポジトリの `.github/workflows/discord.yml` に以下を追加します。

```yaml
name: Discord Issue Notify

on:
  issues:
    types: [opened, closed, deleted]

permissions:
  issues: read
  contents: read

jobs:
  notify:
    uses: Cinnamobot/discord-issue-notify/.github/workflows/notify.yml@main
    secrets:
      DISCORD_WEBHOOK_URL: ${{ secrets.DISCORD_WEBHOOK_URL }}
```

これだけで動きます。

## トリガー

| イベント | 説明 |
|---|---|
| `opened` | Issue が作成されたとき |
| `closed` | Issue がクローズされたとき |
| `deleted` | Issue が削除されたとき |

## ライセンス

MIT
