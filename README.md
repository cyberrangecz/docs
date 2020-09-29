# KYPO CRP

## Dependencies

* `python3.8`
* `pipenv`

## Usage (local server)

```
pipenv sync
pipenv run mkdocs serve
```

Access http://localhost:8000

## Generate Swagger UI *.md file
Make sure you have installed `PyYAML 5.1` or later. If not, use the command:
```
pip install -U PyYAML
``` 
To generate .md file that will be rendered as Swagger UI, use python script `swagger-yaml-to-html.py` as follows: 
```
python swagger-yaml-to-html.py < /path/to/api.yaml > /path/to/generated/file.md
```
