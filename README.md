# mkdocs-page-publisher
Github Action to deploy MkDocs source files as Github Pages, supporting multiple config files.

A template ([mkdocs-template](https://github.com/Kjuly/mkdocs-template)) is available as a demo.

## Usage
The `mkdocs.yml` in the root directory will be used by default.
```yaml
# Sets permissions of the GITHUB_TOKEN to allow deployment to GitHub Pages
permissions:
  contents: read
  pages: write
  id-token: write

jobs:
  publish:
    name: Publish MkDocs Pages
    environment:
      name: github-pages
      url: ${{ steps.deployment.outputs.page_url }}
    runs-on: ubuntu-latest
    steps:
      - name: Checkout
        uses: actions/checkout@v4
      - name: Publish Pages
        id: deployment
        uses: Kjuly/mkdocs-page-publisher@main
        with:
          requirements_file: requirements.txt
```

If you have multiple config files to handle multi-languages, you can provide `config_files`:
```yaml
uses: Kjuly/mkdocs-page-publisher@main
with:
  requirements_file: requirements.txt
  config_files: |-
    config/en/mkdocs.yml
    config/zh-Hans/mkdocs.yml
```

---

If you just want to build pages and deploy to other page hosts, you can use [MkDocs Page Builder][mkdocs-page-builder].


  [mkdocs-page-builder]: https://github.com/Kjuly/mkdocs-page-builder

