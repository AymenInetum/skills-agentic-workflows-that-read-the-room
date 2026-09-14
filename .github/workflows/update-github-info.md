---
name: update-github-info
description: Keep the GitHub information page current with concise updates from GitHub Blog sources.
engine: copilot
on:
  schedule: daily
  workflow_dispatch:
permissions:
  contents: read
tools:
  edit: 
  web-fetch: 
network:
  allowed:
    - github.blog
    - github.com
safe-outputs:
  create-pull-request:
    title-prefix: "[mona] "
    draft: true
    fallback-as-issue: false
    allowed-files:
      - site/content/github-info.md
---

# Update GitHub Information

Read `notes/mona-notes.md` before starting. Fetch both of these sources:

- https://github.blog/latest/
- https://github.blog/changelog/

Using the notes and the fetched sources, update only `site/content/github-info.md` with concise, practical information and source links. Preserve useful existing content when it remains accurate, and do not edit any other file.

When an update is needed, open a draft pull request for Mona to review using the configured `safe-outputs.create-pull-request`. Never write directly to `main`; do not use direct git or GitHub write operations. If no useful, well-supported update is needed, use `noop` with a brief reason.
