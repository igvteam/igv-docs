# Documentation website: IGV desktop application

This repo contains the source for the documentation for the IGV desktop application. The documentation is Markdown based and the website is generated using the [MkDocs](https://www.mkdocs.org/) static site generator. 

To get started, pull this repo and then:
- `conda env create -f igv-docs-env.yml` to install the Conda environment with necessary dependencies.
- `conda activate igv-docs` to activate the environment (the exact command might differ for Anaconda).
- `cd igv-docs`
- `mkdocs serve` to start the MkDocs live-preview web server.
    -  Note: if you get an error concerning ```jinja2``` try the following `pip install jinja2==3.0.0`
    
- `mkdocs build` to build the static site. A subdirectory named `site` will be created.

Note: you might prefer `conda config --set auto_activate_base false`

We're using [Python Markdown](https://python-markdown.github.io/) in the [MkDocs](https://www.mkdocs.org/) static site generator.
With the `extra` [package of extensions](https://python-markdown.github.io/extensions/extra/) we're using it "mostly immitates" 
[PHP Markdown](https://michelf.ca/projects/php-markdown/extra/), do that's a reasonable guide to use.

Be sure to update the `mkdocs.yml` file if you add, remove, or rename any pages since that is where the TOC navigation is defined.
Pages not specified there will be included in the site but not shown in the TOC.

We use the [Windmill template](https://github.com/gristlabs/mkdocs-windmill) for MkDocs.  Refer to that GitHub repository for more details about
template layout, styling, etc.  In particular, we've already made customizations to certain template files (found in the `igv-docs/custom`
folder); the files there override the matching ones from the template.  The full set of template files that can be overridden can be found in
the [mkdocs_windmill](https://github.com/gristlabs/mkdocs-windmill/tree/master/mkdocs_windmill) sub-folder of that repo.  We can copy over and
extend those as well, as needed.

