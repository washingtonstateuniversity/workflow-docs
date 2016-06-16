---
layout: page
title: Deploy WordPress Plugins
---

## Deploy plugins on the WSUWP Platform

Plugins on the WSUWP Platform are grouped into three categories:

1. Individual plugins associated with GitHub repositories.
2. A public collection of plugins not developed at WSU.
3. A private collection of plugins not developed at WSU.

Public plugins are most often available freely at wordpress.org/plugins and have gone through a code review targeting security and performance. Private plugins are usually paid plugins that are not available at wordpress.org/plugins but have also gone through a similar code review.

The WSUWP Platform deployment process is initiated every time a tag is added to a repository. For a full description of the process, see the deployment overview document.

### Individual plugins

### Public plugin collection

The WSU public plugin collection is under the [WSUWP Build Plugins Public](https://github.com/washingtonstateuniversity/WSUWP-Build-Plugins-Public) repository. This can be checked out anywhere on a local machine and contains all of the files for every general public plugin we have installed on the WSUWP Platform.

All changes to the repository are made on the master branch as it is used less for version control and more to organize deployment.

When a plugin update is available, use the following steps:

1. Install or update the plugin in your local development environment and check basics to ensure an incompatibility has not been introduced.
1. Replace the existing plugin files in a local copy of the WSUWP Build Plugins Public repository.
1. Use `git -A plugin-directory` to add all of the changes from the plugin.
1. Write a commit message with the plugin name and version number. (e.g. `Update Query Monitor 2.11.1`).
1. Push the changes on `master` with `git push origin master`.
1. Look at the latest tag number with `git fetch --tags` and then `git tag`
1. Tag the version incrementally. (e.g `git tag -a 00140 -m "Tagging deployment"`)
1. Push the tag to initiate deployment with `git push origin --tags`

With 2 minutes, a Slack notification should appear in #wsuwp with a deployment notification and the latest plugin version will appear on the platform.

### Private plugin collection

The exact same process is used with the [WSUWP Build Plugins Private](https://github.com/washingtonstateuniversity/WSUWP-Build-Plugins-Private) collection, the only caveat being that upgrades are slightly harder to manage due to plugin licensing. Once you have the plugin, deployment follows the exact same steps.
