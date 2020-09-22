[TOC]

MkDocs is a fast, simple and downright gorgeous static site generator that's geared towards building project documentation. Documentation source files are written in Markdown, and configured with a single YAML configuration file `mkdocs.yml`. 

MkDocs require to have installed: 

* python3.8
* pipenv

Clone [repository](https://gitlab.ics.muni.cz/kypo-crp/kypo-crp-project-docs) from Gitlab. To use the local server, go to `kypo-crp-project-docs` directory and in the command line enter the following commands:
```
pipenv sync
pipenv run mkdocs serve
```

Acces the page [http://localhost:8000](http://localhost:8000).

### Pages
To add new page, open file `mkdocs.yml`:
```
site_name: MkLorum
nav:
    - Home: index.md
```


 and add line in `nav` object as follow: 
```
site_name: MkLorum
nav:
    - Home: index.md
    - About: about.md
```

To add nested pages use the following YAML syntax: 
```
site_name: MkLorum
nav:
    - Home: index.md
    - Pages: 
        - Page1: path-to-page1
        - Page2: path-to-page2
```

### Linking to pages
When linking between pages in the documentation you can simply use the regular Markdown linking syntax, including the relative path to the Markdown document you wish to link to.

```
Please see the [project license](license.md) for further details.
```

If the target documentation file is in another directory you'll need to make sure to include any relative directory path in the link.
```
Please see the [project license](../about/license.md) for further details.
```

The toc extension is used by MkDocs to generate an ID for every header in your Markdown documents. You can use that ID to link to a section within a target document by using an anchor link. The generated HTML will correctly transform the path portion of the link, and leave the anchor portion intact.

```
Please see the [project license](about.md#license) for further details.
```

### Linking to images and media

To include images in your documentation source files, simply use any of the regular Markdown image syntaxes:

```
Cupcake indexer is a snazzy new project for indexing small cakes.

![Screenshot](img/screenshot.png)
```

### Tables 
The tables extension adds a basic table syntax to Markdown which is popular across multiple implementations. The syntax is rather simple and is generally only useful for simple tabular data.

A simple table looks like this:
```
First Header | Second Header | Third Header
------------ | ------------- | ------------
Content Cell | Content Cell  | Content Cell
Content Cell | Content Cell  | Content Cell
```
and will be rendered as: 

First Header | Second Header | Third Header
------------ | ------------- | ------------
Content Cell | Content Cell  | Content Cell
Content Cell | Content Cell  | Content Cell


Specify alignment for each column by adding colons to separator lines:
```
First Header | Second Header | Third Header
:----------- |:-------------:| -----------:
Left         | Center        | Right
Left         | Center        | Right
```

### Fenced code blocks
The first line should contain 3 or more backtick (\`) characters, and the last line should contain the same number of backtick characters (\`). The language can optionally be specified on the first line after the backticks which informs any syntax highlighters of the language used: 
~~~~~~~~~~~~~~~~~~~~~
```python
def fn():
    pass
```
~~~~~~~~~~~~~~~~~~~~~

Text wil be rendered as: 
```python
def fn():
    pass
```

### Abbreviations 
Abbreviations are defined using the syntax established in PHP Markdown Extra. The following text: 
```
The HTML specification
is maintained by the W3C.

*[HTML]: Hyper Text Markup Language
*[W3C]:  World Wide Web Consortium
```

will be rendered as: 
The HTML specification
is maintained by the W3C.

*[HTML]: Hyper Text Markup Language
*[W3C]:  World Wide Web Consortium

Move cursor above the abbreviation.

### Footnotes
The Footnotes extension adds syntax for defining footnotes in Markdown documents. The following text: 
```
Footnotes[^1] have a label[^@#$%] and the footnote's content.

[^1]: This is a footnote content.
[^@#$%]: A footnote on the label: "@#$%".
```

will be rendered as:
Footnotes[^1] have a label[^@#$%] and the footnote's content.

[^1]: This is a footnote content.
[^@#$%]: A footnote on the label: "@#$%".

A footnote label must start with a caret ^ and may contain any inline text (including spaces) between a set of square brackets []. Only the first caret has any special meaning.

A footnote content must start with the label followed by a colon and at least one space. The label used to define the content must exactly match the label used in the body (including capitalization and white space). The content would then follow the label either on the same line or on the next line. The content may contain multiple lines, paragraphs, code blocks, blockquotes and most any other markdown syntax. The additional lines must be indented one level (four spaces or one tab).
 

### Notes
Thanks to Admonition extension you are able to create a notes. Following text: 
```
!!! note
    You should note that the title will be automatically capitalized.
```

will be renedered as: 

!!! note
    You should note that the title will be automatically capitalized.

### More extensions
To know more about markdown extension see the MkDocs' [markdown_extensions](https://www.mkdocs.org/user-guide/configuration/#markdown_extensions) configuration setting for details on how to enable extensions.
