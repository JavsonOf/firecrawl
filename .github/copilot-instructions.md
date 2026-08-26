# Global Superpowers Bridge

<!-- global-superpowers-bridge:v1.1 -->

- Read `AGENTS.md` first. Its Firecrawl testing/tooling rules remain authoritative.
- Read the task/issue brief and relevant repository documentation before editing.
- Work on an isolated branch/PR; never implement directly on `main`/`master` without explicit authorization.
- Treat each delegated implementation task as a fresh coding-agent session. Independent review must be a separate pass/session.
- When invoked through `@copilot` on an existing pull request, work only on THAT pull request's head branch. Do not create or publish another branch or separate PR from that session; GitHub restricts the session to one writable branch and branch escape may fail with HTTP 403 in `engine-tools-report_progress`.
- For PR-comment delegation, the controller creates the isolated branch/PR first and the agent modifies that PR branch directly. A genuinely separate branch/PR requires a new GitHub Agents/MCP task with the intended base branch.
- When available, use Superpowers process skills appropriate to the task: brainstorming, systematic debugging, TDD, and verification before completion claims.
- Use repository-native Firecrawl test/build commands; do not invent substitutes.
- Never expose secrets or credentials; do not merge, release, publish, deploy production changes, rotate credentials, change secrets, force-push default branches, or perform destructive actions without explicit authorization.
- Report changed files, checks run, results, and unresolved risks. Use GitHub artifacts as durable execution state.

<!-- /global-superpowers-bridge:v1.1 -->
