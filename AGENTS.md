Firecrawl is a web scraper API. The directory you have access to is a monorepo:
 - `apps/api` has the actual API and worker code
 - `apps/*-sdk` are various SDKs

When making changes to the API, here are the general steps you should take:
1. Write some end-to-end tests that assert your win conditions, if they don't already exist
  - 1 happy path (more is encouraged if there are multiple happy paths with significantly different code paths taken)
  - 1+ failure path(s)
  - Generally, E2E (called `snips` in the API) is always preferred over unit testing.
  - In the API, always use `scrapeTimeout` from `./lib` to set the timeout you use for scrapes.
  - These tests will be ran on a variety of configurations. You should gate tests in the following manner:
    - If it requires fire-engine: `!process.env.TEST_SUITE_SELF_HOSTED`
    - If it requires AI: `!process.env.TEST_SUITE_SELF_HOSTED || process.env.OPENAI_API_KEY || process.env.OLLAMA_BASE_URL`
2. Write code to achieve your win conditions
3. Run your tests using `pnpm harness jest ...`
  - `pnpm harness` is a command that gets the API server and workers up for you to run the tests. Don't try to `pnpm start` manually.
  - The full test suite takes a long time to run, so you should try to only execute the relevant tests locally, and let CI run the full test suite.
4. Push to a branch, open a PR, and let CI run to verify your win condition.
Keep these steps in mind while building your TODO list.

## Global Superpowers Bridge

<!-- global-superpowers-bridge:v1.2 -->

The Firecrawl-specific testing and tooling rules above remain authoritative. In addition:

- Read repository instructions and the GitHub task/issue brief before editing; treat the brief as the source of truth for scope and acceptance criteria.
- Work on the smallest isolated branch/PR. Never implement directly on `main`/`master` without explicit authorization.
- Each delegated implementation task should use a fresh coding-agent session. Independent review must be a separate pass/session.
- When `@copilot` is invoked from an existing pull request, the agent may push only to that pull request's head branch. Never ask that session to create or publish another branch or separate PR; branch escape can fail with HTTP 403 in `engine-tools-report_progress`.
- Controller-first PR-comment delegation: create the isolated branch/PR first, then tell `@copilot` to modify THIS PR branch directly. A genuinely separate branch/PR requires a new GitHub Agents/MCP task with the intended base branch.
- Cloud `@copilot` remains the primary engine. If Copilot quota/credits/plan/entitlement prevents cloud execution, or the user explicitly requests `FORCE BYOK`, use the repository-local v1.2 BYOK runner on the SAME PR head branch via the temporary `.github/superpowers/byok-task.json` trigger.
- BYOK uses the repository Actions `OPENAI_API_KEY` secret through Copilot SDK provider configuration. Never request, expose, commit, log, or place the key in task content; if the secret is missing, report the configuration blocker.
- The BYOK AI session does not own commit/push/merge/release/deploy/secret operations or Bridge governance/runtime files. The workflow wrapper owns the final same-branch commit/push and removes the temporary task file.
- If the standard independent reviewer is unavailable, use a separate read-only `mode: "review"` BYOK task and post its result as a PR comment.
- When Superpowers skills are available, use the relevant process skill before implementation: brainstorming for new behavior/design, systematic debugging for bugs, TDD for features/fixes, and verification before completion claims.
- Follow the repository-native Firecrawl commands above; do not substitute invented test/build commands.
- Never expose credentials or secrets in source, issues, PRs, comments, or logs.
- Do not merge, release, publish, deploy production changes, rotate credentials, change secrets, force-push default branches, or perform destructive operations without explicit authorization.
- Preserve intentional behavior and avoid unrelated refactors.
- Report changed files, checks run, results, and unresolved risks. Use GitHub artifacts as durable execution state.
- Keep implementation and independent review separate; convert blocking review findings into explicit fix work and re-review them.

<!-- /global-superpowers-bridge:v1.2 -->
