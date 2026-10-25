---
name: update-github-info
on:
  schedule: daily
  workflow_dispatch:
permissions:
  contents: read
  copilot-requests: write
engine:
  id: copilot
  copilot-sdk: true
network:
  allowed:
    - github.blog
    - github.com
tools:
  edit:
  web-fetch:
  github:
    toolsets: [repos]
safe-outputs:
  create-pull-request:
    allowed-files:
      - site/content/github-info.md
---

# Update GitHub Info

Keep the GitHub Info page current for Mona and propose every change through a pull request.

1. Read `notes/mona-notes.md` before making any decisions.
2. Use the web-fetch tool to fetch `https://github.blog/latest/`.
3. Use the web-fetch tool to fetch `https://github.blog/changelog/`.
4. Use the GitHub repository API tools to read any repository guidance or reference files needed for this task. Do not use terminal, CLI, or sandboxed commands for those repository reads.
5. Select useful, recent updates for developers, keeping summaries short and practical. Mention the source for each update.
6. Edit only `site/content/github-info.md` with the selected updates.
7. When there are changes, use the `create-pull-request` safe output to open a pull request for Mona to review. Do not write directly to `main`.
