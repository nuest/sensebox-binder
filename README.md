# sensebox-binder

[![Binder](http://mybinder.org/badge.svg)](http://mybinder.org/v2/gh/nuest/sensebox-binder/master)

_A reproducible analysis of environmental data - from hardware to plot!_

This repo can be opened directly in mybinder.org thanks to [this example](https://github.com/binder-examples/dockerfile-rstudio) and [Rocker](https://github.com/rocker-org/binder) by clicking on the "launch binder" button above:

> _To start your RStudio session, click on "new" in the top right, and at the bottom will be RStudio Session. Click that and your RStudio session will begin momentarily!_ [source](https://github.com/binder-examples/dockerfile-rstudio)

The **main workflow** is available both as an R Markdown document (`sensebox-analysis.Rmd`) and a Jypter Notebook using an R kernel (`sensebox-analysis.ipynb`).

The HTML output of the R Markdown document is also rendered by Travis and available [here]().

## Local execution

The following command mounts the current directory to the container's default working directory and exposes the Jupyter port.

```bash
docker run -p 8888:8888 -v $(pwd):/home/rstudio rocker/binder:3.4.2
```

## License

This project is licensed under Apache License, Version 2.0, see file LICENSE.
