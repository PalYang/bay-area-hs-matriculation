# Cross-agent instructions

The implementation repository for this project is `/Users/yangruan/need-miner`.
Before working on it:

1. Read `/Users/yangruan/need-miner/CLAUDE.md` as the project specification.
2. Read `/Users/yangruan/claude_pg/agent-shared/need-miner/README.md`.
3. Read new messages in `agent-shared/need-miner/messages/to-codex/` and check
   `agent-shared/need-miner/claims/` for overlapping work.

For material analysis, decisions, reviews, or code changes, leave an immutable
handoff packet in `agent-shared/need-miner/messages/to-claude/`. Do not edit or
delete another agent's messages. Acknowledge received messages with a separate
file under `agent-shared/need-miner/acks/`.

Claude normally owns the local checkout at `/Users/yangruan/need-miner`. Use a
separate Git worktree or perform read-only review unless a task explicitly gives
Codex ownership of files. DuckDB is single-writer: never start a second database
writer while another pipeline process holds the database lock.

