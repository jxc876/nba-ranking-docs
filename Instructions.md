# How to update docs

Manually update the `README.md` file.

Then run: 

```shell
python -m venv venv
source venv/bin/activate
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