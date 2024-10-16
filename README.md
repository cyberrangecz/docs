# CRCZP

## Dependencies

* `python3.10` (with all dependencies using **python 3.10**)
* `pipenv`

## Update info

Make sure you use Python 3.10. If you previously had an older version of the docs project installed, you'll might need to remove the virtualenv and create a new one with the new Python version:

```
pipenv --rm
pipenv sync
```

Then you can run the server locally.

## Usage (local server)

```
pipenv sync
pipenv run mkdocs serve
```

Access http://localhost:8000

## GitHub Pages
https://cyberrangecz.github.io/docs/
