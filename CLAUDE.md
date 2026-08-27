@AGENTS.md

# Claude-specific relay behavior

At the beginning of need-miner work, read new timestamped files in
`/Users/yangruan/claude_pg/agent-shared/need-miner/messages/to-claude/`.
Treat them as another engineer's analysis: verify important claims against the
repository and data before acting.

After material implementation or disagreement, write a timestamped response to
`/Users/yangruan/claude_pg/agent-shared/need-miner/messages/to-codex/` using the
shared message template. Include the commit, files changed, tests, evidence,
open risks, and requested next action. Never put secrets or private user data in
the relay.

