
<!-- README.md is generated from README.Rmd. Please edit that file -->

# Live Plots with RGL and htmlwidgets in a pkgdown GitHub Pages Site

This package, its GitHub Pages branch the pkgdown site were written for
my own personal reference so that I could remember how to set up a
[pkgdown](https://pkgdown.r-lib.org/) GitHub Pages site with live,
interactive graphics… but you can use it too :).

As of now, **I don’t know of a way to get live plots to show up as live
within the readme itself**– it only works in the vignettes that show up
in the **Articles** section. If you figure this out, let me know.

# Duncan Murdoch’s Work

The nuts and bolts of this package came from [Duncan
Murdoch’s](https://github.com/dmurdoch) work on his [RGL
package](https://github.com/dmurdoch/rgl), without which this wouldn’t
be possible. Although I haven’t met him, Duncan’s work is good and he
should feel good. Note that the LICENSE agreement of this package
includes an agreement to buy him a delicious beverage if you meet him in
person.

# (re-)Integration into pkgdown

It’s my hope that eventually, the functionality that powers live graphs
in pgkdown GitHub Pages sites will become wrapped into the pkgdown
package itself so that pkgdown users can simply add their graphs to
their .Rmd files and push them to their GitHub Pages pkgdown sites
seamlessly. This used to be the case at one point in time; see [pkgdown
Issue \#1689](https://github.com/r-lib/pkgdown/issues/1689).

# SETUP

You could just download or fork this repo and build your site from that,
but the process I used was as follows:

1.  Create an R package that you want to document and publish.
2.  Open RStudio. You probably need to ‘Run as Admin’ – whatever that
    means for your particular OS.
3.  Update all of your packages. Probably should go ahead and make sure
    you’re running the most recent versions of R and RStudio as well.
4.  Install these packages:
    `remotes::install_github(c("r-lib/downlit", "r-lib/pkgdown",       "dmurdoch/rgl", "dmurdoch/htmlwidgets@rglpatch"))`.
5.  Create a new ‘gh-pages’ branch on your repo. Within your shell:

-   checkout/create an orphan branch named “gh-pages”:
    `git checkout --orphan gh-pages`
-   remove everything in “gh-pages” branch: `git rm -rf .`
-   commit the ‘remove all’ and give a commit message:
    `git commit --allow-empty -m 'Initial gh-pages commit'`
-   push it: `git push origin gh-pages`
-   go back to working on your master branch: `git checkout master`

1.  Reboot your computer
2.  Open your project in RStudio again and run
    `usethis::use_pkgdown_github_pages()`
3.  Knit your README.Rmd
4.  Check your DESCRIPTION file and make sure the `SystemRequirements`,
    `VignetteBuilder`, `Imports`, `Depends`, and `Suggests` fields
    include the objects listed in the DESCRIPTION file in this repo (you
    may add more but deleting something may break your site).
5.  You’ll also need to look at the pkgdown.yaml file in
    .github/workflows/ to make sure you’re installing what you need on
    the GitHub server that hosts the pkgdown site.
6.  Make sure you include all the files in /inst required for your site,
    as installed by the pkgdown workflow
7.  run `pkgdown::build_site()` to preview the site. If you get errors,
    check to see if they’re asking you to install packages you don’t
    have, and install them if you need to.
8.  Push to Git.
