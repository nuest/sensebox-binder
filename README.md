# sensebox-binder

[![Binder](http://mybinder.org/badge.svg)](http://mybinder.org/v2/gh/nuest/sensebox-binder/master) [![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.1135140.svg)](https://doi.org/10.5281/zenodo.1135140)

_A reproducible analysis of environmental data - from hardware to plot!_

## One-click execution

This repo can be opened directly in [Binder](https://mybinder.org/) thanks to [this example](https://github.com/binder-examples/dockerfile-rstudio) and [Rocker](https://github.com/rocker-org/binder) by clicking on the "launch binder" button above.

## Local execution

The following commands build a Docker image from the `Dockerfile` and the runs it, which is roughly what happens when launching this repository in Binder.
The current directory (`$(pwd)`) is mounted to the container's default working directory (`/home/rstudio`) and the Jupyter port (`8888`) is exposed to the host computer.

```bash
docker build --tag sensebinder .
docker run -p 8888:8888 -v $(pwd):/home/rstudio sensebinder
```

You are now shown a login link to the Jupyter Notebook, similar to `http://0.0.0.0:8888/?token=bd3fc8b1176293170965e7ce613f5fbfd7a64733f312c34a` but with a different token.
Open this link in your browser and continue with ["Open analysis"](#open-analysis).

## Open analysis

The **main workflow** is available both as an R Markdown document (primary) and a Jupyter Notebook using an R kernel.

To open the **R Markdown document**, click on "new" in the top right, and at "RStudio Session" in the pop-up menu.
This will start a new browser tab with an RStudio session.
In the RStudio window, open the file `sensebox-analysis.Rmd` from the "Files" tab in the bottom right of the interface.
Now click on the ["Knit" button](http://rmarkdown.rstudio.com/authoring_quick_tour.html) to render the document.

For a quick preview, the HTML output of the R Markdown document is also rendered by [Travis CI](http://travis-ci.org/) (see configuration in `.travis.yml`) and available at [https://nuest.github.io/sensebox-binder/sensebox-analysis.html](https://nuest.github.io/sensebox-binder/sensebox-analysis.html).

To open the **Jupyter Notebook**, click on the notebook file `sensebox-analysis.ipynb` on the Jupyter start page.

## Edit analysis

Because the host directory is mounted into the container, all changes to the workflows saved in Jupyter or RStudio are persisted to your local disc.

It is strongly recommended to use only the containerised browser version of RStudio, although the R Markdown document could easily be edited with the desktop version, because working in the container ensures a controlled environment.
To install additional packages, use `install.R` and re-build the container (see ["Local execution"](#local-execution)).

## Export runtime

For the ...

## License

This project is licensed under Apache License, Version 2.0, see file LICENSE.
