---
on:
  issues:
    types: [opened]
permissions:
  contents: read
engine: claude
network:
  allowed:
    - defaults
    - node
safe-outputs:
  add-comment:
    max: 1
  add-labels:
    max: 1
---

# issue-triage

When a new issue is opened, triage it:

1. **Classify** the issue as one of: `bug`, `enhancement`, `question`, or `documentation`.
2. **Add the matching label** to the issue using safe-outputs add-labels.
3. **Post a friendly comment** using safe-outputs add-comment that:
   - Greets the author by their GitHub username
   - Summarizes your understanding of the issue in one or two sentences
   - If it is a bug report missing reproduction steps, expected behavior, or environment details, politely ask for the missing information
   - Keep the comment short and helpful

**Important:** Do not close or edit the issue. Only classify, label, and comment using safe-outputs tools.

Example comment:
> Hi @author-username! Thanks for opening this issue. I understand you're experiencing [brief summary]. To help us better understand and fix this, could you please share [missing details]?

For non-bug issues:
> Hi @author-username! Thanks for the [enhancement/question/documentation] contribution. I understand you're suggesting [brief summary]. This looks [relevant assessment].
