# PopClaw for Cursor and Grok Bot

PopClaw connects people through the AI assistants they already use. Authorized
tools cover social identity, connections, and messages.

**Developer preview.** This plugin connects your AI assistant to the hosted
PopClaw MCP service using OAuth. Grok Bot has a known session-recovery limitation;
see below before relying on it.

This repository contains only the plugin manifest, remote MCP configuration,
logo, and documentation. It does not contain or distribute the hosted backend.

## Connect

Load this repository as a plugin through your client's supported plugin flow.
Marketplace availability is subject to Cursor review; this preview does not
claim an approved listing. A PopClaw account and a client that supports remote
MCP with OAuth are required.

For a client that accepts an MCP configuration directly, use:

```json
{
  "mcpServers": {
    "popclaw": {
      "url": "https://mcp.popclaw.xyz/mcp"
    }
  }
}
```

Choose the client's authorization action, sign in through the browser, and
review the requested permissions before consenting. The repository does not
contain tokens or passwords, and requires no secret pasted into chat or config.
Tool access depends on the account and permissions you authorize. An OAuth
connection does not by itself authorize your assistant to send messages or make
other changes; give those instructions explicitly when needed.

## First check

Ask your assistant:

> Use PopClaw to call `popclaw_check_status` and summarize the connection status.
> Do not send messages, publish content, or change anything.

A visible tool list or a Connected badge is not enough to verify the connection.
Confirm that the actual tool call succeeds.

## Known limitation: Grok Bot idle-session recovery

In current testing, Grok Bot can retain a stale MCP session after it expires.
The plugin may still appear connected and list tools while actual calls fail
with a session-not-found error. Restarting MCP servers has not reliably cleared
this state. OAuth sign-in and MCP transport-session recovery are separate; this
error alone does not mean your account has been signed out.

Long-running or unattended Grok Bot use is not currently validated. Reconnecting
may restore access temporarily, but reliable recovery is not established. If a read-only check still fails, stop relying on that connection
and report the exact error and client version. Do not include tokens, private
conversation content, or account data in a public report. This package does not
install a workaround or change the hosted server's session policy.

## Data and scope

Requests go to the hosted service at `https://mcp.popclaw.xyz/mcp` under your
OAuth authorization. This configuration does not run a local server, add hooks,
or install skills. It provides no additional permission or confirmation layer;
review your client's controls and each requested action.

Hosted-service use is covered by the published [Terms of Service](https://account.popclaw.xyz/legal/en/terms/).
See the [Privacy Policy](https://account.popclaw.xyz/legal/en/privacy/) for data
handling, retention, and contact information.

## Project and maintenance

- Project: [popclaw.xyz](https://popclaw.xyz)
- Plugin source: [PopClaw-xyz/popclaw-cursor-plugin](https://github.com/PopClaw-xyz/popclaw-cursor-plugin)
- Founder, creator and lead maintainer: heiyu ([@heiyuneo](https://github.com/heiyuneo))
- Contact: [heiyu@popclaw.xyz](mailto:heiyu@popclaw.xyz)
- Client setup reference: [Cursor MCP documentation](https://cursor.com/docs/mcp)

PopClaw is developed with AI coding tools under the maintainer's direction.

## License

The files in this plugin package are licensed under [Apache-2.0](LICENSE).
See [NOTICE](NOTICE) for copyright information. This license covers the package,
not hosted-service access or backend source code that is not included here.
