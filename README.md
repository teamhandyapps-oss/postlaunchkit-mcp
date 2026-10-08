# PostLaunchKit MCP

Hosted MCP server for the [PostLaunchKit directory](https://postlaunchkit.com/directory/): a human-reviewed directory of free tools and projects, including AI agent tooling. Run by Team Handyapps.

- Endpoint: `https://postlaunchkit.com/mcp`
- Transport: Streamable HTTP (JSON-RPC over POST), stateless, no sessions
- Auth: none
- Cost: free

There is nothing to install. The server is hosted, and this repo only documents it.

## Tools

| Tool | What it does | Arguments |
| --- | --- | --- |
| `search_projects` | Search published directory entries | `query`, `category`, `tag`, `page` (all optional) |
| `get_project` | Get one published entry by slug | `slug` (required) |
| `list_categories` | List categories with entry counts | none |
| `submit_project` | Suggest a product. Saved to a pending queue and reviewed by a person; nothing is published automatically | `name`, `url`, `one_liner`, `why_try`, `category` (required); `tags`, `contact`, `agent_name` (optional) |
| `run_launch_check` | Run the free launch check on a public website. Returns how many checks passed, each check with a pass or fail status and a fix for failures, and a report link | `url` (required) |
| `list_launch_directories` | List directories and listing sites where an indie product can be submitted, from the open [launch-directories dataset](https://postlaunchkit.com/launch-directories/) (CC BY 4.0). Blank values mean not verified | `free`, `dofollow`, `requires_account`, `ai_agent_friendly`, `query` (all optional) |

Submissions are limited per IP and per day, and a duplicate domain is rejected. `run_launch_check` is limited to 20 checks per IP per day and only checks public sites.

## Client config

Most MCP clients that support remote servers accept a config like this:

```json
{
  "mcpServers": {
    "postlaunchkit": {
      "url": "https://postlaunchkit.com/mcp"
    }
  }
}
```

## Quick check

```bash
curl -s -X POST https://postlaunchkit.com/mcp \
  -H 'content-type: application/json' \
  -d '{"jsonrpc":"2.0","id":1,"method":"tools/list"}'
```

## Other ways in

- Agent guide: https://postlaunchkit.com/for-agents/
- OpenAPI spec for the REST API: https://postlaunchkit.com/openapi.json
- llms.txt: https://postlaunchkit.com/llms.txt
- Directory: https://postlaunchkit.com/directory/

## Licence

MIT. See [LICENSE](LICENSE). Copyright Team Handyapps.
