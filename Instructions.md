# Docs

How to update the docs and generate the site.

First, update the Markdown files.

Then run: 

```shell
python -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
```

To preview locally:

```shell
mkdocs serve
```

To publish:

```shell
mkdocs gh-deploy
```