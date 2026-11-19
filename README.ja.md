# Ritomira MCP

[English](README.md)

AI アプリを [Ritomira](https://ritomira.com) に MCP でつなぎます。Claude や ChatGPT などに X の投稿の成績を聞き、次の投稿の下書きや予約まで、チャットの中で進められます。

このリポジトリにあるのは**接続の手順と設定の例だけ**です。MCP のサーバーは Ritomira が運営しているので、インストールや起動は要りません。

| | |
|---|---|
| 接続先の URL | `https://mcp.ritomira.com/mcp` |
| 通信方式 | Streamable HTTP |
| 認証 | OAuth（ブラウザで Ritomira にログイン。API キーは使いません） |
| 公式の MCP Registry | [`com.ritomira/ritomira`](https://registry.modelcontextprotocol.io/) |
| 対応する SNS | X。Instagram・Threads・Facebook ページは対応予定です |
| プラン | Standard 以上。一部の分析（投稿のテーマ）は Pro 以上です。[料金](https://ritomira.com/pricing) |

## 頼めること

- 「先週の投稿は、その前の週と比べてどうだった？」
- 「今月よく見られた投稿と、その共通点を教えて」
- 「反応が多いのは何曜日の何時？」
- 「うまくいった投稿をもとに下書きを3つ作って、いちばん良いものを木曜の9時に予約して」

## 権限と安全

- **最初は読み取りだけです。** つないだ直後は、投稿と分析を読むことしかできません。
- **それ以上の操作は、ご自身でオンにします。** 下書きや予約などは、Ritomira の設定で接続ごとにオンにします。変えたあとは、AI アプリからつなぎ直してください。
- **取り消せない操作は、人が承認します。** X での返信・フォロー、コメントへの返信、X の記事の公開は、AI アプリに出る確認の画面で、ご本人が承認します。確認の画面を出せないアプリからは、これらの操作はできません。
- **いつでも切断できます。** Ritomira の設定から切断すると、次の呼び出しから使えなくなります。

詳しくは[セキュリティとデータの扱い](https://ritomira.com/security)をご覧ください。

## つなぎ方

### Claude（デスクトップ・Web）

1. Claude で **カスタマイズ → コネクタ** を開き、カスタムコネクタを追加します。
2. 名前を `Ritomira` にして `https://mcp.ritomira.com/mcp` を入れます。OAuth でつなぎ、Ritomira にログインして、アカウントと許す操作を確かめます。
3. Claude で Ritomira を有効にして、[最初のお願い](#最初のお願い)を送ります。

組織で使っている場合は、管理者がカスタムコネクタを許可する必要があることがあります。[Claude の手順](https://support.claude.com/en/articles/11175166-get-started-with-custom-connectors-using-remote-mcp)

### Claude Code

```bash
claude mcp add --transport http --scope user ritomira https://mcp.ritomira.com/mcp
```

そのあと Claude Code で `/mcp` を開き、`ritomira` を選んでブラウザで認証します。[Claude Code の手順](https://code.claude.com/docs/en/mcp)

### ChatGPT（Web）

1. ChatGPT で、カスタムの MCP サーバーを追加します。
2. 名前を `Ritomira` にして `https://mcp.ritomira.com/mcp` を入れ、OAuth を選びます。
3. Ritomira にログインし、アカウントと許す操作を確かめて、有効にします。

使える設定は、ChatGPT のプランやワークスペースの設定によって変わります。[OpenAI の手順](https://developers.openai.com/api/docs/guides/custom-mcp-server)

### Codex CLI

```bash
codex mcp add ritomira --url https://mcp.ritomira.com/mcp
codex mcp login ritomira
```

Codex で `/mcp` を開いて、つながっているかを確かめます。外すときは `codex mcp remove ritomira` です。[Codex の手順](https://developers.openai.com/codex/mcp)

### そのほかのアプリ

`https://mcp.ritomira.com/mcp` を、リモートの HTTP（Streamable HTTP）の MCP サーバーとして追加し、OAuth を始めます。JSON の例は [`examples/mcp.json`](examples/mcp.json) にあります。Streamable HTTP と OAuth に対応したアプリが必要です。すべてのアプリで動作を確かめたわけではありません。

## 最初のお願い

まずは読み取りだけのお願いで、つながったかを確かめます。

> Ritomira につないでいる SNS のアカウントを、名前と SNS の種類つきで一覧にして。複数あれば、どれを使うか聞いて。読み取りの操作だけにして。

## つながらないとき

- **「上位のプランが必要」と出る**：MCP は Standard 以上で使えます。プランを変えたら、つなぎ直してください。
- **下書きや予約が使えない**：Ritomira の設定でオンにしてから、つなぎ直してください。
- **認証をもう一度求められる**：アプリの MCP の設定からつなぎ直し、Ritomira にログインしてください。

## リンク

- [MCP 連携の案内](https://ritomira.com/features/mcp)（道具の一覧と権限の詳細）
- [Ritomira](https://ritomira.com)
- [お問い合わせ](https://ritomira.com/contact)

運営：合同会社NeXus AI
