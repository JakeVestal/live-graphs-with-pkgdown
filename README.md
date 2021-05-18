
<!-- README.md is generated from README.Rmd. Please edit that file -->

# Live Plots and htmlwidgets in a pkgdown GitHub Pages Site

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

``` r
remotes::install_github(
  c(
    "r-lib/downlit", "r-lib/pkgdown", 
    "dmurdoch/rgl", "dmurdoch/htmlwidgets@rglpatch"
  )
)
```

1.  Create a new ‘gh-pages’ branch on your repo:

<!-- -->

    git checkout --orphan gh-pages
    git rm -rf .
    git commit --allow-empty -m 'Initial gh-pages commit'
    git push origin gh-pages
    git checkout master

1.  Reboot your computer
2.  run `usethis::use_pkgdown_github_pages()`
3.  Knit your README.Rmd
4.  Check your DESCRIPTION file and make sure the `SystemRequirements`,
    `VignetteBuilder`, `Imports`, `Depends`, and `Suggests` fields
    include the objects listed in the DESCRIPTION file in this repo (you
    may add more but deleting something may break your site).
5.  run `pkgdown::build_site()` to preview the site
6.  Push to Git.

## INTRODUCTION

The RGL package is a visualization device system for R, using OpenGL or
WebGL as the rendering backend. An OpenGL rgl device at its core is a
real-time 3D engine written in C++. It provides an interactive viewpoint
navigation facility (mouse + wheel support) and an R programming
interface. WebGL, on the other hand, is rendered in a web browser; rgl
produces the input file, and the browser shows the images.

## WEBSITE

A `pkgdown` website is here:

<https://dmurdoch.github.io/rgl/>

The unreleased development version website is here:

<https://dmurdoch.github.io/rgl/dev/>

See [this
vignette](https://dmurdoch.github.io/rgl/dev/articles/pkgdown.html) for
details on producing your own `pkgdown` website that includes `rgl`
graphics.

The currently active development site is here:

<https://github.com/dmurdoch/rgl>

## INSTALLATION

Most users will want to install the latest CRAN release. For Windows,
macOS and some Linux platforms, installation can be easy, as CRAN
distributes binary versions:

    # Install latest release from CRAN
    install.packages("rgl")

To install the latest development version from Github, you’ll need to do
a source install. Those aren’t easy! Try

    # Install development version from Github
    remotes::install_github("dmurdoch/rgl")

If that fails, read the instructions below.

## LICENSE

The software is released under the GNU Public License. See
[COPYING](./COPYING) for details.

## FEATURES

-   portable R package using OpenGL (if available) on macOS, Win32 and
    X11
-   can produce 3D graphics in web pages using WebGL
-   R programming interface
-   interactive viewpoint navigation
-   automatic data focus
-   geometry primitives: points, lines, triangles, quads, texts, point
    sprites
-   high-level geometry: surface, spheres
-   up to 8 light sources
-   alpha-blending (transparency)
-   side-dependent fill-mode rendering (dots, wired and filled)
-   texture-mapping with mipmapping and environment mapping support
-   environmental effects: fogging, background sphere
-   bounding box with axis ticks marks
-   undo operation: shapes and light-sources are managed on type stacks,
    where the top-most objects can be popped, or any item specified by
    an identifier can be removed

## PLATFORMS

macOS Windows 7/10 Unix-derivatives

## BUILD TOOLS

R recommended tools (gcc toolchain) On Windows, Rtools40 (or earlier
versions for pre-R-4.0.0)

## REQUIREMENTS

**For OpenGL display:**

Windowing System (unix/x11 or Windows)  
OpenGL Library  
OpenGL Utility Library (GLU)

**For WebGL display:**

A browser with WebGL enabled. See <https://get.webgl.org>.

## Installing OpenGL support

**Debian:**  
aptitude install libgl1-mesa-dev libglu1-mesa-dev

**Fedora:**  
yum install mesa-libGL-devel mesa-libGLU-devel libpng-devel

**macOS:**  
Install XQuartz.  
`rgl` should work with either XQuartz 2.7.11 or 2.8.0, but it will
probably need rebuilding if the XQuartz version changes. XQuartz
normally needs re-installation whenever the macOS version changes.

**Windows:**  
Windows normally includes OpenGL support, but to get the appropriate
include files etc., you will need the appropriate version of
[Rtools](https://cran.r-project.org/bin/windows/Rtools/) matched to your
R version.

## Options

The **libpng** library version 1.2.9 or newer is needed for pixmap
import/export support.

The **freetype** library is needed for resizable anti-aliased fonts. On
Windows, it will be downloaded from <https://github.com/rwinlib> during
the install.

## BUILDING/INSTALLING

Binary builds of `rgl` are available for some platforms on CRAN.

For source builds, install the prerequisites as described above,
download the tarball and at the command line run

R CMD INSTALL rgl\_0.106.19.tar.gz

(with the appropriate version of the tarball). The build uses an
`autoconf` configure script; to see the options, expand the tarball and
run `./configure --help`.

Alternatively, in R run

install.packages(“rgl”)

to install from CRAN, or

remotes::install\_github(“dmurdoch/rgl”)

to install the development version from Github.

## BUILDING WITHOUT OPENGL

As of version 0.104.1, it is possible to build the package without
OpenGL support on Unix-alikes (including macOS) with the configure
option –disable-opengl For example,

R CMD INSTALL –configure-args=“–disable-opengl” rgl\_0.106.19.tar.gz

On Windows, OpenGL support cannot currently be disabled.

## DOCUMENTATION and DEMOS:

    library(rgl)
    browseVignettes("rgl")
    demo(rgl)

## CREDITS

Daniel Adler <dadler@uni-goettingen.de>  
Duncan Murdoch <murdoch@stats.uwo.ca>  
Oleg Nenadic <onenadi@uni-goettingen.de>  
Simon Urbanek <simon.urbanek@math.uni-augsburg.de>  
Ming Chen <mchen34@uwo.ca>  
Albrecht Gebhardt <albrecht.gebhardt@uni-klu.ac.at>  
Ben Bolker <bolker@zoo.ufl.edu>  
Gabor Csardi <csardi@rmki.kfki.hu>  
Adam Strzelecki <ono@java.pl>  
Alexander Senger <senger@physik.hu-berlin.de>  
The R Core Team for some code from R.  
Dirk Eddelbuettel <edd@debian.org>  
The authors of Shiny for their private RNG code.  
The authors of `knitr` for their graphics inclusion code. Jeroen Ooms
for `Rtools40` and `FreeType` help.  
Yohann Demont for Shiny code, suggestions, and testing.  
Joshua Ulrich for a lot of help with the Github migration.  
Xavier Fernandez i Marin for help debugging the build.  
George Helffrich for draping code.  
Ivan Krylov for window\_group code in X11.
