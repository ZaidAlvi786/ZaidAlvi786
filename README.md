name: Generate Snake

on:
  schedule:
    - cron: "0 */24 * * *"
  workflow_dispatch:
  push:
    branches:
      - main

jobs:
  generate:
    permissions:
      contents: write
    runs-on: ubuntu-latest
    steps:
      - uses: Platane/snk/svg-only@v3
        with:
          github_user_name: ZaidAlvi786
          outputs: |
            dist/github-contribution-grid-snake-dark.svg?palette=github-dark&color_snake=#8A2BE2&color_dots=#1a1a2e,#4B0082,#6A0DAD,#7B2CBF,#8A2BE2

      - uses: crazy-max/ghaction-github-pages@v3.1.0
        with:
          target_branch: output
          build_dir: dist
        env:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
