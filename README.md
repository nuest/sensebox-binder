# sensebox-binder

[![Binder](http://mybinder.org/badge_logo.svg)](http://mybinder.org/v2/gh/nuest/sensebox-binder/master) [![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.1135139.svg)](https://doi.org/10.5281/zenodo.1135139)

_A reproducible analysis of environmental data - from hardware to plot!_

The analysis can be explored in three ways, all of which offer full transparency and provide an interactive environment to [study and adopt](#edit-analysis) code and data.

1. [One-click execution](#one-click-execution)
1. [Local build and execution](#local-build)
1. [Import runtime and local execution](#import-runtime)

## One-click execution

This repo can be opened directly in [Binder](https://mybinder.org/) thanks to [this example](https://github.com/binder-examples/dockerfile-rstudio) and [Rocker](https://github.com/rocker-org/binder) by clicking on the "launch binder" button above.

[![screencast of senseBox-Binder analysis in RStudio running on mybinder.org](https://media.giphy.com/media/l49JRjO65S0WQ1Kyk/giphy.gif)](https://media.giphy.com/media/l49JRjO65S0WQ1Kyk/giphy.gif)

## Local build

The following commands build a Docker image from the `Dockerfile` and the runs it on your local machine.
Therefore you need [Docker](http://docker.com/).
The steps are roughly what happens when launching this repository in Binder.

```bash
docker build --tag sensebinder .
```

Continue with [Local execution](#local-execution).

## Import runtime

[Zenodo](https://en.wikipedia.org/wiki/Zenodo) is a public research data repository.
It provides a secure place to deposit datasets and makes them citable by providing a [DOI](https://en.wikipedia.org/wiki/Digital_object_identifier).

This workflow relies on several online resources and tools that might disappear or stop working (GitHub, openseSenseMap-API, Docker, ...), but Zenodo is much less likely to vanish.

Download all files from [https://doi.org/10.5281/zenodo.1135140](https://doi.org/10.5281/zenodo.1135140) and put them in one directory.

Import the runtime from the compressed tarball (cf. [Export runtime](#export-runtime)).

```bash
docker image load --input sensebox-binder.tar.gz
```

Continue with [Local execution](#local-execution).

## Local execution

You have now either build or loaded a Docker image.
Now start a Docker container using the image with the following command.

```bash
docker run -p 8888:8888 -v $(pwd):/home/rstudio sensebinder
```

The current directory (`$(pwd)` for Ubuntu/Debian; on Windows or Mac please manually put in the local path) is mounted to the container's default working directory (`/home/rstudio`) and the Jupyter port (`8888`) is exposed to the host computer.
You may leave out the mount, but changes are not persisted to the host machine then.

The output includes a login link to the Jupyter Notebook start page, similar to `http://0.0.0.0:8888/?token=bd3fc8b1176293170965e7ce613f5fbfd7a64733f312c34a` but with a different token.
Open this link in your browser and continue with [Open analysis](#open-analysis).

### Troubleshooting

If you encounter file permission errors, such as `PermissionError: [Errno 13] Permission denied: '/home/rstudio/.local'` when starting the container, try to explicitly set the container user ID to the required default user `rstudio` with `UID` of `1000`.

```bash
docker run -it -p 8888:8888 --user=1000 sensebinder
```

## Open analysis

The **main workflow** is available both as an [R Markdown](http://rmarkdown.rstudio.com/) document (primary) and a [Jupyter Notebook](https://nbformat.readthedocs.io/en/latest/) (automatic conversion) using an R kernel.

To open the **R Markdown document**, click on "new" in the top right, and at "RStudio Session" in the pop-up menu.
This will start a new browser tab with an RStudio session.
In the RStudio window, open the file `sensebox-analysis.Rmd` from the "Files" tab in the bottom right of the interface.
Now click on the ["Knit" button](http://rmarkdown.rstudio.com/authoring_quick_tour.html) to render the document.

For a quick preview, the HTML output of the R Markdown document is also rendered by [Travis CI](http://travis-ci.org/) (see configuration in `.travis.yml`) and available at [https://nuest.github.io/sensebox-binder/sensebox-analysis.html](https://nuest.github.io/sensebox-binder/sensebox-analysis.html).

To open the **Jupyter Notebook**, click on the notebook file `sensebox-analysis.ipynb` on the Jupyter start page.
The Jupyter Notebook is automatically updated when rendering the R Markdown document.

## Edit analysis

Because the host directory is mounted into the container, all changes to the workflows saved in Jupyter or RStudio are persisted to your local disc.

It is strongly recommended to use only the containerised browser version of RStudio, although the R Markdown document could easily be edited with the desktop version, because working in the container ensures a controlled environment.
To install additional packages, use `install.R` and re-build the container (see [Local execution](#local-execution)).

## Export runtime

The following steps were used to create the archivable version of the workflow stored on Zenodo (cf. [Import runtime](#import-runtime)).

First create a [Local build](#local-build).
Then export the container using it's name with the `docker image save` command into a [compressed](https://en.wikipedia.org/wiki/Gzip) [tarball](https://en.wikipedia.org/wiki/Tar_(computing)):

```bash
docker image save sensebinder:latest | gzip -c > sensebox-binder.tar.gz
```

The created image contains the runtime environment of the workflow (R, Jupyter Notebook, libraries & packages) as well as files from this directory, including the [git repository](https://en.wikipedia.org/wiki/Git).

## Create release

1. Create a [Local build](#local-build) and start a [Local execution](#local-execution) without mounting the local files
1. Make sure the R Markdown document renders correctly with `online <- FALSE` in the code chunk `load_box_data`, then set `online <- TRUE` again and re-render
1. Commit all changes to the git repository
1. Add a tag `v1` to the current git commit and push the tag to GitHub
1. Start a [Local execution](#local-execution) with mounting the local files to render the R Markdown document to HTML;make sure the hash in the HTML file is the one with the version tag
1. Create a [Local build](#local-build) (to have the latest commit and tag in the local git repository)
1. [Export runtime]("#export-runtime")
1. Create ZIP file with `zip -1 -r sensebox-binder.zip .git data .dockerignore .gitignore .travis.yml 320px-Fireworks_2.jpg Dockerfile install.R LICENSE README.md sensebox-analysis.* sensebox-binder.Rproj sensebox-binder.tar.gz` (fast compression, the tarball is already compressed and the other file sizes are negligible)
1. Upload to Zenodo (as a new version), setting the same version tag

## Contact

[Daniel Nüst](https://nordholmen.net), [@nordholmen](https://twitter.com/nordholmen), [https://orcid.org/0000-0002-0024-5046](https://orcid.org/0000-0002-0024-5046)

## License

This project is licensed under Apache License, Version 2.0, see file LICENSE.
