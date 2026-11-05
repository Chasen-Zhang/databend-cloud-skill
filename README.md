# Databend Cloud Skill

Query data, analyze performance, and manage Databend Cloud with your AI agent.

For **Databend Cloud**, not self-hosted Databend. Requires an agent that can read skills and execute commands, Python 3, and HTTPS access to the Cloud API. No MCP server or third-party Python packages are required. `jq` is optional, only for readable log exports.

## Install and set up with your agent

Paste this prompt into your agent. It installs the skill and guides API key setup without asking you to put the key in chat.

```text
Install the databend-cloud skill:
https://github.com/databendcloud/databend-cloud-skill

Follow SKILL.md to reuse an API key or help me save one for https://api.databend.com.
Keep the key out of chat. Stop after setup; do not connect or run SQL.
```

The skill reuses supported credentials or guides private terminal input. Credentials stay outside the installation directory, under `~/.config/databend-cloud/` by default, with separate keys for each API origin. A remote agent needs credentials in its actual execution environment. See [Authentication](references/authentication.md).

Install only one source of `databend-cloud` per agent to avoid duplicate or conflicting copies.

## After setup

Ask your agent to connect to the intended organization and warehouse, then try:

- “Summarize sales trends this month.”
- “Show me the tables in this database.”
- “Help me optimize this SQL query.”

The agent resolves saved targets or asks for the missing Organization ID. The warehouse is `default` unless you select another. See [Connection workflow](references/connection.md) and [Organization and target selection](references/organizations.md).

## Security and permissions

- Keep API keys out of chat, command arguments, and repository files. Local credential files are private but not encrypted.
- Configure the token's IP allowlist for the agent's actual public egress IP. An empty allowlist means no IP restriction.
- Tokens follow the account's current organization role. Database privileges enforce access; the skill is not a read-only sandbox.
- Writes, destructive SQL, permission changes, and compute changes require confirmation. Investigation is read-only.
- Query results and logs may enter the agent's model context.

See [Authentication](references/authentication.md), [API capabilities](references/api-capabilities.md), and [Errors and recovery](references/errors.md).

## Development

Run the existing offline tests from the repository root. They use synthetic fixtures, not live Cloud credentials:

```bash
python3 -m unittest discover -s scripts -p '*_test.py'
```

The skill entrypoint is [SKILL.md](SKILL.md). Scripts and tests remain in `scripts/`; task-specific guides remain in `references/`.

## Source and license

Derived from [`evotai/evot-skills`, `skills/databend-cloud`](https://github.com/evotai/evot-skills/tree/ad14e1fde0570e12354d92f61960e076f3186714/skills/databend-cloud), retaining its Apache-2.0 license and version history. This repository is maintained independently; changes are not automatically synchronized with the evot version.

See [LICENSE](LICENSE) and [CHANGELOG.md](CHANGELOG.md) for the license and standalone changes.
