---
name: ai-code-review
description: Review pull requests for bugs, security vulnerabilities, performance issues, and code quality. Use when the user asks for code review, PR review, audit, or wants AI feedback on a diff or pull request.
---

# AI Code Review

Automated code review: read the PR diff, find real problems, and attach inline comments with severity ratings.
## Input
Accept any of: GitHub PR link, branch name to diff against main, or pasted code/diff snippet.
## Review Categories
### P0 - Critical
- Security: hardcoded secrets, SQL injection, XSS, path traversal, unsafe deserialization
- Data loss: destructive operations without confirmation, missing transactions
- Crash risk: nil/null dereference, unhandled promise rejection, infinite recursion
### P1 - High
- Bugs: off-by-one, inverted conditions, missing edge cases, race conditions
- Performance: N+1 queries, missing indexes, sync IO in hot paths, memory leaks
- Error handling: swallowed errors, bare except, missing retry logic
### P2 - Medium
- Code quality: duplicated logic, overly complex functions, magic numbers
- Naming: misleading variable names, inconsistent conventions
- Missing tests: changed logic without test coverage
Do NOT flag style issues or personal preference.
## Workflow
1. Read PR title and description
2. Fetch diff via gh CLI
3. Analyze file by file against all categories
4. Emit ::code-comment for each finding
5. Print summary with APPROVED / CHANGES REQUESTED verdict
## Inline Comment Format
::code-comment{title="[PX] Issue name" body="One-paragraph explanation with fix." file="/path/to/file.ts" start=LINE priority=N}
Priority values: 0 for P0, 1 for P1, 2 for P2.
## Summary Format
**Review Summary** - Files: N, P0(critical): N, P1(high): N, P2(medium): N, Overall: APPROVED/CHANGES REQUESTED
## Language Checks
Python: type confusion, mutable defaults, exception handling.
JS/TS: async/await misuse, undefined access, prototype pollution.
Go: error handling, goroutine leaks, nil map access.
Rust: unsafe blocks, unwrap misuse, lock ordering.
Java/Kotlin: null safety, resource leaks, thread safety.
SQL: missing WHERE, missing indexes, injection.
