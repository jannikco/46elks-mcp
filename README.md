# 46elks MCP server

Check the telecom account and explicitly approve one SMS to an authorized recipient.

A direct-provider MCP server with useful local execution. No PipMCP account is required for local use. Provider API access and any provider charges are your responsibility.

## Quick start

Requires Node.js22+. Clone this repository, then run:

```sh
npm ci --ignore-scripts
npm test
npm start
```

The default command inspects the tools offline. Configure your own credentials in your environment:

- `ELKS46_API_USERNAME`
- `ELKS46_API_PASSWORD`



Credential help: https://46elks.com/docs/overview

## Execute a real read

Replace example record IDs with records you are authorized to access.

```sh
npm start -- --call elks46_get_account '{}'
```

## Use with an MCP client

Launch `node /absolute/path/46elks-mcp/server.mjs` using stdio transport; pass credentials through the client environment. Stdout is reserved for JSON-RPC.

## Tools

| Tool | Effect | Purpose |
| --- | --- | --- |
| elks46_get_account | Read | elks46 get account |
| elks46_send_sms | Explicit approval required | Send one SMS to an explicitly authorized recipient; consumes provider credits. |

## Concrete workflow

Check the telecom account and explicitly approve one SMS to an authorized recipient.

1. elks46_get_account
2. elks46_send_sms

## Optional writes

Writes are disabled by default. Set CONNECTOR_ALLOW_WRITES=true and supply `_approval: {approved:true,idempotencyKey:"unique-request-id"}` on the specific call. Do not reuse a key for a different request. Uncertain outcomes are never automatically replayed; inspect the provider before another attempt.

## Capability evidence

Local: **Tested — HTTP fixtures and real stdio tools/call**. Managed: **Documented**. Provider authentication and live operations have not been established by these fixture tests. Evidence applies per operation and execution mode; setup discovery does not imply provider execution.

## Managed production

[Activate with PipMCP](https://pipmcp.com/github/start?app=46elks&integration=46elks-mcp&utm_source=github&utm_campaign=github-46elks-mcp&utm_content=readme) when you want the hosted service.  Local credentials are not uploaded by this code. Review provider permissions in the managed onboarding. [Directory and related projects](https://jannikco.github.io/pipmcp-connectors/integrations/46elks/).

## Provenance and maintenance

- https://46elks.com/docs/send-sms
- https://46elks.com/docs/me

Maintainer:jannikco. MIT license for this code. See connector.json for selected operations and integration.json for evidence. Runtime dependencies retain their own licenses. Report sensitive issues through https://pipmcp.com/contact; do not post credentials or customer data in public issues.
