name: Update README date

on:
  push:
    branches: [main]
    paths-ignore:
      - 'README.md'
      - '.github/**'

permissions:
  contents: write

jobs:
  update-date:
    runs-on: ubuntu-latest
    if: github.actor != 'github-actions[bot]'
    steps:
      - name: Checkout
        uses: actions/checkout@v4

      - name: Update last-updated marker
        run: |
          DATE=$(date -u +"%B %Y")
          sed -i "s|<!-- LAST-UPDATED -->.*<!-- /LAST-UPDATED -->|<!-- LAST-UPDATED -->${DATE}<!-- /LAST-UPDATED -->|" README.md

      - name: Commit & push if changed
        run: |
          git config user.name "github-actions[bot]"
          git config user.email "41898282+github-actions[bot]@users.noreply.github.com"
          git add README.md
          git diff --staged --quiet || (git commit -m "chore: auto-update README date" && git push)
