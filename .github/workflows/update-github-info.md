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
  playwright:
network:
  allowed:
    - github.blog
    - github.com
    - awesome-copilot.github.com
safe-outputs:
  create-pull-request:
    title-prefix: "[mona] "
    draft: true
    fallback-as-issue: false
    allowed-files:
      - site/content/github-info.md
---

# Update GitHub Information

Read `notes/mona-notes.md` before starting. Fetch all of these sources:

- https://github.blog/latest/
- https://github.blog/changelog/
- https://awesome-copilot.github.com/workflows/

Using the notes and the fetched sources, update only `site/content/github-info.md` with concise, practical information and source links. Preserve useful existing content when it remains accurate, and do not edit any other file.

When an update is needed, open a draft pull request for Mona to review using the configured `safe-outputs.create-pull-request`. Never write directly to `main`; do not use direct git or GitHub write operations. If no useful, well-supported update is needed, use `noop` with a brief reason.

Use the provided Playwright browser to read the three required source URLs.
Follow the installed Playwright instructions and keep all network requests
within the configured allowed domains.

Read the actual page content before updating site/content/github-info.md.
Do not substitute invented information for unavailable sources.
If the sources remain inaccessible, report the task as incomplete using
safeoutputs report_incomplete, with the exact error.