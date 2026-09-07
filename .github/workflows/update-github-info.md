---
name: update-github-info
description: Keep Mona's GitHub Info content current with practical, official GitHub updates.
model: gpt-5.4
on:
  schedule: daily
  workflow_dispatch:
permissions:
  contents: read
tools:
  edit: true
  web-fetch:
  github:
    mode: local
    toolsets: [repos]
network:
  allowed:
    - github.blog
    - github.com
    - awesome-copilot.github.com
safe-outputs:
  create-pull-request:
    title-prefix: "[mona] "
    draft: false
    allowed-files:
      - site/content/github-info.md
---

# Update GitHub Info

Read `notes/mona-notes.md` before drafting any content. Use the GitHub repository API tools to read repository guidance and reference files; do not use terminal, CLI, or sandboxed commands for those repository reads.

Fetch these official public sources with the web-fetch tool:

- https://github.blog/latest/
- https://github.blog/changelog/
- https://awesome-copilot.github.com/workflows/

Include Awesome Copilot workflows among the sources when selecting useful, recent items.

Identify useful, recent items that fit Mona's editorial angle. Keep summaries short and practical for developers, mention whether each item comes from the GitHub Blog or GitHub Changelog, and include the source URL. Update only `site/content/github-info.md`, preserving its existing structure and adding or refreshing concise entries rather than replacing useful existing guidance.

When there are meaningful supported changes, use the configured `create-pull-request` safe output to open a pull request for Mona to review. Do not write directly to the default branch. If the sources contain no meaningful new information or the evidence is insufficient, use `noop` with a short reason instead of opening an empty pull request.