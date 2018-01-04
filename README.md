# sensebox-binder

[![Binder](http://mybinder.org/badge.svg)](http://mybinder.org/v2/gh/nuest/sensebox-binder/master)

_A reproducible analysis of environmental data - from hardware to plot!_

This repo can be opened directly in [Binder](https://mybinder.org/) thanks to [this example](https://github.com/binder-examples/dockerfile-rstudio) and [Rocker](https://github.com/rocker-org/binder) by clicking on the "launch binder" button above:

> _To start your RStudio session, click on "new" in the top right, and at the bottom will be RStudio Session. Click that and your RStudio session will begin momentarily!_ [source](https://github.com/binder-examples/dockerfile-rstudio)

The **main workflow** is available both as an R Markdown document (`sensebox-analysis.Rmd`) and a Jupyter Notebook using an R kernel (`sensebox-analysis.ipynb`).

The HTML output of the R Markdown document is also rendered by Travis and available at [https://nuest.github.io/sensebox-binder/sensebox-analysis.html](https://nuest.github.io/sensebox-binder/sensebox-analysis.html).

## Local execution

The following commands build a Docker image and the runs it, mounting the current directory to the container's default working directory and exposing the Jupyter port.

```bash
docker build --tag sensebinder .
docker run -p 8888:8888 -v $(pwd):/home/rstudio sensebinder
```

It is strongly recommended to use this setup to get RStudio, and _not edit the R Markdown file locally_, because working in the container means a controlled environment and the above approach is what happens on BinderHub.
To install additional packages, use `install.R`.

## Tipps

To create both R Markdown and Jupyter Notebook the following [notedown](https://github.com/aaren/notedown) can help create a notebook file for manual adjustments:

```bash
notedown sensebox-analysis.Rmd --knit --nomagic > output.ipynb
```

## License

This project is licensed under Apache License, Version 2.0, see file LICENSE.
