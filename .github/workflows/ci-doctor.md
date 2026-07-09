---
name: CI Doctor
on:
  workflow_run:
    workflows: ["CI"]
    types: [completed]
    branches: [main]
permissions:
  contents: read
  actions: read
  issues: read
  pull-requests: read
tools:
  github:
safe-outputs:
  create-issue:
    max: 1
---

# CI Doctor

Investigate CI workflow failures on the main branch.

**Only proceed if the workflow conclusion is "failure".**

When the "CI" workflow completes with a failure on the main branch:

1. **Download the logs** of the failed jobs from that workflow run.
2. **Identify** which step and which test failed, and extract the relevant error message.
3. **Read** the failing test file and the source file under test to find the root cause.
4. **Create an issue** titled "CI failure: <short root cause>" using safe-outputs create-issue containing:
   - A one-paragraph diagnosis in plain English
   - The relevant log excerpt (trimmed to the essential lines)
   - The file and line where the bug likely is
   - A suggested fix as a code snippet
   - A link to the failed workflow run

**Important:** If an open issue for the same root cause already exists, do not create a duplicate. Check existing issues first before creating a new one.
