
[![CircleCI](https://img.shields.io/circleci/project/github/ncar-hackathons/jupyterlab-tutorial/master.svg?style=for-the-badge&logo=circleci)](https://circleci.com/gh/ncar-hackathons/jupyterlab-tutorial)


# JupyterLab Tutorial

JupyterLab Tutorial



## Building and Previewing Site Locally


Once you’ve added content to `content` directory and udpated the table of contents in `_data/toc.yml`, it’s time to build the raw material that Jekyll will turn into a website. 


### Build the site’s markdown


To Build your site's markdown, make sure to have `jupyter-book` package installed. `jupyter-book` can be installed from PyPI with pip:

```bash
pip install jupyter-book
```

Once `jupyter-book` is installed, run the following command:

```bash
jupyter-book build JupyterLab Tutorial/
```

This will:

- Use the links specified in the `_data/toc.yml` file (pointing to files in `/content/`) and do the following:

  - Run nbconvert to turn the .ipynb files into markdown
  - Replace relative image file paths so that they work on your new built site
  - Clean up formatting issues for things like MathJax to display properly
  - Place all these generated files in the `JupyterLab Tutorial/_build/`
  
  
Note that jupyter-book will automatically update any files in `_build/` that are older than the timestamp of the corresponding file in your `content`/ folder.
  
### Previewing site Locally
  
Once you’ve generated the markdown for your notebooks and installed the necessary dependencies. You are ready to build your site HTML.

Ensure that your notebooks have been converted to markdown, there should be a collection of them in `_build/.directory`.
  
  
First, you’ll need to make sure you have Docker installed. There are installation instructions for [each operating system to guide you through this process](https://hub.docker.com/search/?type=edition&offering=community).

Once Docker is available on your system, you can build the image locally with:

```
docker pull emdupre/jupyter-book
```

You can then access this image with:

```
docker run --rm --security-opt label:disable  \
   -v /full/path/to/your/JupyterLab Tutorial-dir:/srv/jekyll \
   -p 4000:4000 \
   -it -u 1000:1000 \
   emdupre/jupyter-book bundle exec jekyll serve --host 0.0.0.0
```

If you navigate to http://0.0.0.0:4000/JupyterLab Tutorial/ in your browser, you should see a preview copy of the site. 
