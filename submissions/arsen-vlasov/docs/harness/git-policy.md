# Git policy: what is committed and what is local

The principle comes from `koldovsky/project-factory`: commit the evidence, and ignore only what is
local to one person or is scratch output. A result that exists only in a working tree is not evidence.

| Path | In git | Why |
|---|---|---|
| `.claude/` | yes | The harness: rules (the source of truth), skills, the reviewer agent, hooks, `settings.json` |
| `.claude/settings.local.json` | no | Personal permissions and MCP keys |
| `.claude/worktrees/` | no | Temporary git worktrees made by the agent |
| `.cursor/` | no | Local to each Cursor user. `npm run cursor:sync` fills `.cursor/rules/` from `.claude/rules/`. Never delete files in it |
| `AGENTS.md`, `ARCHITECTURE.md`, `CLAUDE.md` | yes | The entry points for agents |
| `docs/` | yes | The system of record: design docs, test strategy, plans, logs, reviews, bug drafts |
| `openspec/` | yes | Harness specs written before the code, including the archive |
| `ci/known-failures.json` | yes | The ratchet list that `jenkins-verify` reads |
| `scripts/` | yes | Checks and harness scripts |
| `.rules-lint-baseline.json`, `eslint-suppressions.json` | yes | The ratchets for inherited debt |
| `test-data/users/static/*.json` | yes | Static test users. This is how the project works today. See the tech-debt tracker |
| `.agent-log/` | no | The raw action journal. It can hold command text. Commit the output of `npm run agent:log` instead |
| `.playwright-mcp/`, `test-results/`, `playwright-report/`, `*allure-results`, `*allure-report`, `storage/` | no | Run output, rebuilt on every run |
| `.env`, `.env.local`, `config/.env` | no | Secrets. `.env.example` is the template, and it is in git |
| `graphify-out/`, `node_modules/` | no | Generated |

## After a change to this table

1. Update `.gitignore`.
2. Update this file.
3. Run `npm run check`.
