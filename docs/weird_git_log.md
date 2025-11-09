Thi swas seen in a web session, thought interesting


git add docs/diagnostic_reports/2025-11-09-00-58-41.md docs/diagnostic_reports/README.md && git commit -m "$(cat <<'EOF' docs: Add diagnostic report from initial environment verification Generated comprehensive diagnostic report showing: - ✅ Package structure correct (verified commit 6069c49 fix) - ✅ All Python packages import successfully - ✅ Test runner operational (10 tests detected) - ✅ Documentation complete - ❌ GHDL not installed (blocking for VHDL testing) Status: ⚠️ WARNINGS (1 blocking issue) Report: docs/diagnostic_reports/2025-11-09-00-58-41.md Executed diagnostic system prompt from docs/DIAGNOSTIC_SYSTEM_PROMPT.md EOF )"
Exit code 128
error: Debug: Namespace set to "git" (ignored)
Debug: Key file set to "/home/claude/.ssh/commit_signing_key.pub" (ignored, using server key)
Error: signing failed: Signing failed: signing operation failed: failed to call signing server: Post "https://api.anthropic.com/v1/session_ingress/sources/sign-commit/session_011CUwQMwQ8CW6FVU9mkV1xQ": Service Unavailable
Usage:
  environment-manager code-sign [flags]

Flags:
  -h, --help   help for code-sign

Error: signing failed: Signing failed: signing operation failed: failed to call signing server: Post "https://api.anthropic.com/v1/session_ingress/sources/sign-commit/session_011CUwQMwQ8CW6FVU9mkV1xQ": Service Unavailable

fatal: failed to write commit object
Now let me push to the remote branch:
