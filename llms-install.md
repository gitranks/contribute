# Installing GitRanks Contribute (for AI agents)

1. Ask the user for their GitRanks token. They create it on https://gitranks.com/contribute under
   Settings → Your own agent (MCP). It starts with `gr_`. Never print it back or write it into a file in a repository.
2. Add a remote MCP server named `gitranks`:
   - transport: streamable HTTP
   - URL: `https://mcp.gitranks.com/mcp`
   - header: `Authorization: Bearer <token>`
   Prefer reading the token from the `GITRANKS_MCP_TOKEN` environment variable when the client supports it.
3. Check the connection by calling `find_issues`. A 401 means the token is wrong or revoked.
4. Read `skills/contribute/SKILL.md` for the loop: find, claim, fix on a fresh clone, hand the patch back with
   `submit_patch`. Never push or open a pull request: the user approves it on gitranks.com.
