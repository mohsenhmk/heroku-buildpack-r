# Heroku and Cloud Foundry buildpack: R

This is a Cloud Foundry and Heroku buildpack for applications which use
[R](http://www.r-project.org/) for statistical computing and [CRAN](http://cran.r-project.org/) for R packages.  It is nearly identical to a previous version of the Heroku buildpack which is compatible with Shiny.  As of May 18, 2016, the current version of the Heroku buildpack may not be fully compatable with Shiny, [details here](https://github.com/virtualstaticvoid/heroku-buildpack-r/issues/56).  

R is ‘GNU S’, a freely available language and environment for statistical computing and graphics which provides
a wide variety of statistical and graphical techniques: linear and nonlinear modelling, statistical tests, time
series analysis, classification, clustering, etc. Please consult
the [R project homepage](http://www.r-project.org/) for further information.

[CRAN](http://cran.r-project.org/) is a network of ftp and web servers around the world that
store identical, up-to-date, versions of code and documentation for R.

## Usage
The buildpack will detect your app makes use of R if it has the `init.r` file in the root.
The R runtime is vendored into your slug, and includes the gcc compiler for fortran support.

## Installing R packages
During the slug compilation process, the `init.r` R file is executed. Put code in this file to install any packages you may require.
See the [Installing-packages](http://cran.r-project.org/doc/manuals/R-admin.html#Installing-packages) for details. The
list of available packages can be found at [http://cran.r-project.org](http://cran.r-project.org/web/packages/available_packages_by_date.html).

```
# Example `init.r` file

install.packages("nlme", dependencies = TRUE)

```

R packages can also be included in your project source and installed when the `init.r` file is executed.

```
install.packages("optional-path-to-packages/local-r-package-file.tar.gz", repos=NULL, type="source")
```

## R Binaries
The binaries used by the buildpack are hosted on AWS S3 at [s3://heroku-buildpack-r](https://heroku-buildpack-r.s3.amazonaws.com).

See the [heroku-buildpack-r-build](https://github.com/virtualstaticvoid/heroku-buildpack-r-build) repository for building the R binaries yourself.

## R Versions
Optionally, the R version and buildpack version can be configured by providing a `.r-version` and `.r-buildpack-version` file in the root directory.
These files should contain 1 line of text containing the respective version. See [alternate-versions](https://github.com/virtualstaticvoid/heroku-buildpack-r/tree/cedar-14/test/alternate-versions) for an example.

The following versions are available:

### Cedar 10

| R Version | Buildpack Version | Binary |
|-----------|-------------------|--------|
| 2.15.1    | 20131211-0028     | [R-2.15.1-binaries-20131211-0028.tar.gz](https://heroku-buildpack-r.s3.amazonaws.com/cedar/R-2.15.1-binaries-20131211-0028.tar.gz) |
| 3.0.2     | 20140218-0019     | [R-3.0.2-binaries-20140218-0019.tar.gz](https://heroku-buildpack-r.s3.amazonaws.com/cedar/R-3.0.2-binaries-20140218-0019.tar.gz ) |
| 3.1.0     | 20141127-0021     | [R-3.1.0-binaries-20141127-0021.tar.gz](https://heroku-buildpack-r.s3.amazonaws.com/cedar/R-3.1.0-binaries-20141127-0021.tar.gz ) |
| 3.1.2     | 20150301-1046     | [R-3.1.2-binaries-20150301-1046.tar.gz](https://heroku-buildpack-r.s3.amazonaws.com/cedar/R-3.1.2-binaries-20150301-1046.tar.gz ) |

NB: Remember to use the `http://github.com/virtualstaticvoid/heroku-buildpack-r.git#cedar` branch for the buildpack URL.

### Cedar 14

| R Version | Buildpack Version | Binary |
|-----------|-------------------|--------|
| 3.1.0     | 20150303-1543     | [R-3.1.0-binaries-20150303-1543.tar.gz](https://heroku-buildpack-r.s3.amazonaws.com/cedar-14/R-3.1.0-binaries-20150303-1543.tar.gz) |
| 3.1.2     | 20150428-2302     | [R-3.1.2-binaries-20150428-2302.tar.gz](https://heroku-buildpack-r.s3.amazonaws.com/cedar-14/R-3.1.2-binaries-20150428-2302.tar.gz) |
| 3.1.3     | 20150718-2347     | [R-3.1.3-binaries-20150718-2347.tar.gz](https://heroku-buildpack-r.s3.amazonaws.com/cedar-14/R-3.1.3-binaries-20150718-2347.tar.gz) |
| 3.2.0     | 20150719-0018     | [R-3.2.0-binaries-20150719-0018.tar.gz](https://heroku-buildpack-r.s3.amazonaws.com/cedar-14/R-3.2.0-binaries-20150719-0018.tar.gz) |
| 3.2.1     | 20151119-2338     | [R-3.2.1-binaries-20151119-2338.tar.gz](https://heroku-buildpack-r.s3.amazonaws.com/cedar-14/R-3.2.1-binaries-20151119-2338.tar.gz) |
| 3.2.2     | 20151120-0000     | [R-3.2.2-binaries-20151120-0000.tar.gz](https://heroku-buildpack-r.s3.amazonaws.com/cedar-14/R-3.2.2-binaries-20151120-0000.tar.gz) |
| 3.2.3     | 20151214-2343     | [R-3.2.2-binaries-20151214-2343.tar.gz](https://heroku-buildpack-r.s3.amazonaws.com/cedar-14/R-3.2.3-binaries-20151214-2343.tar.gz) |
| 3.2.4     | 20160322-0811     | [R-3.2.2-binaries-20160322-0811.tar.gz](https://heroku-buildpack-r.s3.amazonaws.com/cedar-14/R-3.2.4-binaries-20160322-0811.tar.gz) |

NB: Remember to use the `http://github.com/virtualstaticvoid/heroku-buildpack-r.git#cedar-14` branch for the buildpack URL.

## Caveats
Due to the size of the R runtime, the slug size on Heroku, without any additional packages or program code, is approximately 90Mb.
If additional R packages are installed by the `init.r` script then the slug size will increase.

## Credits
Original inspiration from [Noah Lorang's Rook on Heroku](https://github.com/noahhl/rookonheroku) project.

## License
MIT License. Copyright (c) 2013 Chris Stefano. See MIT_LICENSE for details.
