---
layout: page
title: Deploy WordPress Themes
---

## Overview

Themes on the WSUWP Platform are grouped into two categories:

1. Individual themes associated with GitHub repositories.
2. A public collection of themes not developed at WSU.

Public themes are most often available freely at wordpress.org/themes and have gone through a code review targeting security and performance.

The WSUWP Platform deployment process is initiated every time a tag is added to a repository. For a full description of the process, see the [WSUWP Deployments plugin](https://github.com/washingtonstateuniversity/WSUWP-Deployment) documentation.

## Individual themes

The set up and deployment processes for individual themes are covered in the [Overview](https://github.com/washingtonstateuniversity/WSUWP-Deployment#overview) section of the WSUWP Deployments documentation.

## Public theme collection

The WSU public theme collection is under the [WSUWP Build Themes Public](https://github.com/washingtonstateuniversity/WSUWP-Build-Themes-Public) repository. This can be checked out anywhere on a local machine and contains all of the files for every general public theme we have installed on the WSUWP Platform.

All changes to the repository are made on the master branch as it is used less for version control and more to organize deployment.

When a theme update is available, use the following steps:

1. Install or update the theme in your local development environment and check basics to ensure an incompatibility has not been introduced.
1. Replace the existing theme files in a local copy of the WSUWP Build Themes Public repository.
1. Use `git -A theme-directory` to add all of the changes from the theme.
1. Write a commit message with the theme name and version number. (e.g. `Update Make 1.7.4`).
1. Push the changes on `master` with `git push origin master`.
1. Look at the latest tag number with `git fetch --tags` and then `git tag`
1. Tag the version incrementally. (e.g `git tag -a 00140 -m "Tagging deployment"`)
1. Push the tag to initiate deployment with `git push origin --tags`

With 2 minutes, a Slack notification should appear in #wsuwp with a deployment notification and the latest theme version will appear on the platform.
