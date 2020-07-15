# Step away from the notebook!
## Use an R package to organize your project
[Jim Tyhurst](https://www.jimtyhurst.com)<br>
2020-07-14

I will give an overview of the advantages of using the R package structure for a data science project, even when you will never publish the package for reuse by others. I have a few discussion points about how package structure improves the development lifecycle. There is also a list of references with more details.

Topics that are only mentioned here, but really deserve their own full length discussion as good practices for software development of any type, including data science projects:

* Use source control.
* Write unit tests (and other types of tests).
* Automate a build process.

For now, we are just considering the advantages of using an R package to organize a project.

---

**Contents**

* [Advantages to using an R package for your project files](#advantages-to-using-an-r-package-for-your-project-files)
* [Disadvantages](#disadvantages)
* [References: Use the R package structure to organize your projects](#references-use-the-r-package-structure-to-organize-your-projects)
* [References: R package structure](#references-r-package-structure)
* [References: workflow for R development and reproducibility](#references-workflow-for-r-development-and-reproducibility)

---

## Advantages to using an R package for your project files
* Access to automated tools
    * documenting
    * building
    * testing
        * unit testing while coding
        * automated Continuous Integration (CI) testing
    * checking
* A standard for where to store files.
    * R code (functions) in the `R/` directory.
    * R Markdown in the `vignettes/` directory.
        * Some people put exploratory data analysis scripts or markdown in a `research/` folder.
    * Metadata, data about your project:
        * A `README.md` displays by default on the home page of the project if you use one of the Git repository providers to store your project. e.g. [GitHub](https://github.com/), [GitLab](https://gitlab.com/), [BitBucket](https://bitbucket.org/), [Framagit](https://framagit.org/), etc.
            * Note: All of the Git repository providers allow you to have private repositories if you do not want to expose your work publicly.
        * Dependencies in the `DESCRIPTION` file.
        * A license should be specified in the `DESCRIPTION` file.
            * Depending on the license, you may also want a `LICENSE` file.
    * Data: It depends! See section [12. External data](https://r-pkgs.org/data.html) of [R Packages, 2nd edition](https://r-pkgs.org/):
        * `data/` directory is for binary data to be exposed as part of the package, such as the output of `save` or `saveRDS`. See `usethis::use_data()`.
        * `data-raw/` directory is for reproducibility. It includes original data and the scripts you used to transform it into the clean data that you expose in the `data/` directory. See `usethis::use_raw_data()`.
        * `inst/extdata/` for raw data, e.g. CSV files, used in vignettes.
        * `tests/testthat/` for small data files used for unit testing.
* Easy to share your code and analyses with others.
    * You provide a standard structure, so people know where to look for details, like dependencies, the license, the reusable code, the tests, ...
* Easy to deploy your code.
    * While any code can be deployed to a different machine, it is especially easy to use a package in a Docker image to deploy an application to a server.

## Disadvantages
* It takes some time and effort to learn package structure ... but automated tools make it easy to get started:
    * The {[usethis](https://usethis.r-lib.org/index.html)} package is very helpful.
    * The [R Packages, 2nd edition](https://r-pkgs.org/) book provides clear explanations. It is a great reference for getting started, as well as getting deeper into package structure.
* It takes some time to set up each new package. Even with the automated tools, you still need to enter your custom information. However, I am convinced that the benefit of package structure for improving developer workflow is much greater than this small cost of set-up.


## References: Use the R package structure to organize your projects
* Ben Marwick, Carl Boettiger, Lincoln Mullen. 2018-03-20. [Packaging data analytical work reproducibly
using R (and friends)](https://peerj.com/preprints/3192/). [PDF](https://peerj.com/preprints/3192.pdf).
    * "The purpose of this paper is to show how the R package can be a suitable template for organising files into a research compendium to enhance the reproducibility of research."
* Denis Gontcharov. 2020-02-28. [Put your Data Analysis in an R Package — Even if You Don’t Publish it](https://towardsdatascience.com/put-your-data-analysis-in-an-r-package-even-if-you-dont-publish-it-64f2bb8fd791): How to leverage R's package development environment to organize, document and test your work.
    * Working on our analysis inside an R package offers four benefits:
        1. R packages provide a standardized folder structure to organize your files
        2. R packages provide functionality to document data and functions
        3. R packages provide a framework to test your code
        4. putting effort into points 1–3 enables you to reuse and share your code
* Anna Krystalli. March-April 2020. [Reproducible Research Data & Project Management in R](https://annakrystalli.me/rrresearchACCE20/). See especially the [Paths and Project structure](https://annakrystalli.me/rrresearchACCE20/path-proj-str.html) section.
    * An earlier workshop provides lots of good details too: Anna Krystalli. 2018-10-31. [Manage functionality as a package](https://annakrystalli.me/rrtools-repro-research/package.html). This is part 3 of a 4 part workshop: [Reproducible Research in R with `rrtools`](https://annakrystalli.me/rrtools-repro-research/index.html).
* Edwin Thoen. 2020. [Agile Data Science with R: A workflow](https://edwinth.github.io/ADSwR/index.html). See [6.1 Using the R Package Structure](https://edwinth.github.io/ADSwR/code-organisation.html)
    * Highlights presented by Edwin Thoen at: Invited Speakers Session 1.  2020-06-17. "Building Agile data products leveraging the R package structure". [eRum 2020](https://2020.erum.io/). Individual talks have not been published separately yet, but this talk appears at 1:54:10 - 2:12:00 of the complete [Day 1 recording](https://www.youtube.com/watch?v=yHJ7RSv6nio).
* Colin Fay, et al. 2020-07-07. [Engineering Production-Grade Shiny Apps](https://engineering-shiny.org/). See [3.1 Shiny App as a Package](https://engineering-shiny.org/structure.html).


## References: R package structure
* Hadley Wickham. 2015. [R Packages](http://r-pkgs.had.co.nz/).
* Hadley Wickham, Jenny Bryan. in process. [R Packages, 2nd edition](https://r-pkgs.org/).
* Scott Chamberlain. 2018-10-01. [R package development workshop](https://portlandrusergroup.github.io/pkgdev/). Presented at [Portland R User Group](https://www.meetup.com/portland-r-user-group/events/253797396/) Meetup on 2018-09-27.
* Maëlle Salmon. 2020-04-29. [Workflow automation tools for package developers](https://blog.r-hub.io/2020/04/29/maintenance/).
* Maëlle Salmon. 2020. [How to improve your R package: Automatically, and not](https://maelle.github.io/erum2020/index.html#1). Presented at [e-Rum 2020](http://2020.erum.io/) Invited Speakers Session 3. 2020-06-19. Individual talks have not been published separately yet, but this talk appears at 5:39:22 - 5:53:20 of the complete [Day 3 recording](https://www.youtube.com/watch?v=ZRGxTHRY_hs).
* [rOpenSci](https://ropensci.org/) software review editorial team. 2020-07-13. [rOpenSci Packages: Development, Maintenance, and Peer Review](https://devguide.ropensci.org/). See especially [Chapter 1. Packaging Guide](https://devguide.ropensci.org/building.html).


## References: workflow for R development and reproducibility
* Hilary Parker. 2017-08-30. [Opinionated analysis development](https://peerj.com/preprints/3210/). [PeerJ Preprints 5:e3210v1](https://doi.org/10.7287/peerj.preprints.3210v1). [PDF](https://peerj.com/preprints/3210v1.pdf).
* Edwin Thoen. 2020. [Agile Data Science with R: A workflow](https://edwinth.github.io/ADSwR/index.html).
* Riccardo Porreca, Peter Schmid, Andrea Melloncelli. 2020-06-20. Bring your R Application Safely to Production: Collaborate, Deploy, Automate. Workshop at [e-Rum 2020](https://2020.erum.io/program/workshops/).
    * [MLflow Documentation](https://mlflow.org/docs/latest/index.html).
* Anna Krystalli. 2020-07-10. [Computational Reproducibility: from theory to practice](https://www.youtube.com/watch?v=KHMW8fV2NXo). Keynote lecture at useR! 2020.
* [Research Compendia](https://research-compendium.science/) web site has a "Resources" section with papers and talks that touch on templates and workflows for reproducible research.
* The Turing Way. [Guide for Reproducible Research](https://the-turing-way.netlify.app/reproducible-research/reproducible-research.html). See especially the [Reproducible environments](https://the-turing-way.netlify.app/reproducible-research/renv.html) section for useful principles, although examples are for Python, not R.