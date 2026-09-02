# Tseha MCP Server

**Serves your design system and coding standards to coding agents, so they stop guessing.**

Tseha is a hosted, remote MCP server. Point your coding agent at it and the agent reads your
real component APIs, design tokens and coding standards instead of inventing them.

- **Website:** <https://tseha.io>
- **Documentation:** <https://tseha.io/docs>
- **MCP endpoint:** `https://tseha.io/mcp` (Streamable HTTP)
- **Official MCP Registry name:** `io.tseha/tseha`

This repository holds the published `server.json` manifest and the connection documentation.
Tseha itself is a hosted commercial service and its source is not open; there is nothing to
install or build here.

## Quick start

Add a `.mcp.json` to the root of your repository:

```json
{
  "mcpServers": {
    "tseha": {
      "url": "https://tseha.io/mcp"
    }
  }
}
```

That is the whole configuration. On first connection the agent opens an OAuth sign-in in your
browser. Approve it once and the agent is connected.

### Other clients

| Client | Where the config lives |
| --- | --- |
| Claude Code | `.mcp.json` in the project root, or `claude mcp add --transport http tseha https://tseha.io/mcp` |
| Cursor | `.cursor/mcp.json` (per project) or `~/.cursor/mcp.json` (global) |
| VS Code / GitHub Copilot, and any other MCP client | point at `https://tseha.io/mcp` over the HTTP transport |

### Cursor plugin

This repository is also packaged as a Cursor plugin (`.cursor-plugin/plugin.json`
plus `mcp.json`), so Cursor can install the connection for you instead of you
editing a config file. Install it from **Cursor Settings -> Plugins**, or add the
repository by hand from <https://cursor.directory/plugins>.

## Authentication

**OAuth 2.1 with PKCE (S256).** There is no API key to paste. Tseha publishes the standard
discovery documents — `/.well-known/oauth-authorization-server` and
`/.well-known/oauth-protected-resource` (RFC 9728) — and supports both Dynamic Client
Registration and Client ID Metadata Documents, so compliant clients configure themselves.

The issued token is scoped to your organization and your role. **The MCP surface is read-only
for every role.** Writes happen only in the Tseha admin panel.

## Tools

All nine tools are read-only. Every tool except `list_projects` takes a `project_id`, which
`list_projects` returns.

| Tool | What it returns |
| --- | --- |
| `list_projects` | The projects in your organization, each with id, name and framework. Call this first — the id is required by every other tool. |
| `list_packages` | The component packages assigned to a project, with version, and which one is active. |
| `list_components` | Every UI component in the project's design system: name, source package, import path, intended use. |
| `get_component` | The full spec for one component: import path, props schema, usage example, anti-patterns, when-to-use notes, Figma spec, dependencies. |
| `search_components` | Components ranked by description, for finding one by need rather than by name. |
| `get_style` | Style metadata for a design token collection. |
| `get_style_tokens` | Design tokens by category: color, typography, spacing, radius, shadow, blur, or all. |
| `get_standards` | Your organization's development standards, by section (global, react, nextjs, …). |
| `get_component_updates` | What changed between the installed version of a component and the current one. |

## Protocol conformance

- MCP revision **2026-07-28**, Streamable HTTP transport
- OAuth 2.1 + PKCE S256 (mandatory), RFC 9728 protected-resource metadata, RFC 9207 `iss` on
  authorization responses, RFC 8252 §7.3 loopback redirect URIs
- Dynamic Client Registration and Client ID Metadata Documents

## Registry

Published to the [official MCP Registry](https://registry.modelcontextprotocol.io) under the
DNS-verified namespace `io.tseha`:

```bash
curl -s "https://registry.modelcontextprotocol.io/v0/servers?search=tseha"
```

## License

The manifest and documentation in this repository are published under the
[MIT licence](LICENSE).

That licence covers the contents of this repository only. It does not grant any
licence to the Tseha service at <https://tseha.io>, which is a hosted commercial
product governed by its own terms, nor any right to use the Tseha name or logo
as a trademark.

## Support

Questions and issues: <https://tseha.io/docs>, or open an issue on this repository.
