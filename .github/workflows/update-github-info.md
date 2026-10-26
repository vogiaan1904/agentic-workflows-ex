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
  model: gpt-4.1
  copilot-sdk: true
network:
  allowed:
    - github.blog
    - github.com
    - awesome-copilot.github.com
tools:
  edit:
  bash: ["curl"]
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
4. Use the web-fetch tool to fetch `https://awesome-copilot.github.com/workflows/`.
5. If web-fetch is unavailable because Copilot is running in offline API-proxy mode, use the bash tool with `curl --fail --location --allow-url` for each of the three approved URLs. Do not use any other network access.
6. Use the GitHub repository API tools to read any repository guidance or reference files needed for this task. Do not use terminal, CLI, or sandboxed commands for those repository reads.
7. Select useful, recent updates for developers, keeping summaries short and practical. Mention the source for each update.
8. Edit only `site/content/github-info.md` with the selected updates.
9. When there are changes, use the `create-pull-request` safe output to open a pull request for Mona to review. Do not write directly to `main`.
