# Hello world!

This page serves as display of mathematical formulae.

Trying to find out what's required to display formulae...

## Solution

* Install `pymdown-extensions` locally;
* Update `mkdocs.yml` with 
  ```
  - pymdownx.arithmatex:
      generic: true`
  ```
  added to `markdown_extensions:`.
  
  Further more, add
  ```
  extra_javascript:
  - javascripts/config.js
  - https://polyfill.io/v3/polyfill.min.js?features=es6
  - https://cdn.jsdelivr.net/npm/mathjax@3/es5/tex-mml-chtml.js
  ```
  in the `yml` file;
* Update `docs/requirements.txt` and add the require packages.
