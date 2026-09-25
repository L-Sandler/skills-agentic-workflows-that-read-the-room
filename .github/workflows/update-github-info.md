---
name: update-github-info
description: Keep the GitHub Info website current with practical updates from official GitHub sources.
on:
  schedule:
    - cron: "17 9 * * *"
  workflow_dispatch:
permissions:
  contents: read
engine: copilot
model: gpt-5.6-luna-free-auto
tools:
  github:
    toolsets:
      - repos
  web-fetch:
  edit:
network:
  allowed:
    - github.blog
    - github.com
    - awesome-copilot.github.com
safe-outputs:
  create-pull-request:
    max: 1
    draft: false
---

# Update GitHub Info

Maintain the GitHub Info website through a reviewable pull request for Mona.

## Instructions

1. Use the GitHub repository API tools to read `notes/mona-notes.md`, `site/content/github-info.md`, and any repository guidance or reference files needed for this task. Do not use terminal, CLI, or sandboxed shell commands to read repository guidance or reference files.
2. Use `web-fetch` to read `https://github.blog/latest/`, `https://github.blog/changelog/`, and `https://awesome-copilot.github.com/workflows/`.
3. Select the most useful recent updates for Mona's practical, developer-focused editorial angle. Prefer official sources, keep summaries short, and include source links in the page.
4. Use the `edit` tool to update `site/content/github-info.md`. Preserve its existing structure and update only what is supported by the fetched sources and repository notes.
5. Review the resulting change for accuracy, clarity, and unnecessary churn.
6. Use the `create_pull_request` safe output exactly once to open a pull request for Mona to review. The pull request should describe the sources consulted and summarize the content changes. Do not write directly to `main`, push manually, or merge the pull request.

If no meaningful, well-supported update is available, leave `site/content/github-info.md` unchanged and do not create a pull request.
