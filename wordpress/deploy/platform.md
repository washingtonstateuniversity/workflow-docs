---
layout: page
title: Deploy WordPress Updates to the Platform
---

## Overview

WordPress is updated through the [WSUWP-Platfom repository](https://github.com/washingtonstateuniversity/WSUWP-Platform). These steps presume that a local environment has been set up using the instructions documented there. It also assumes that the [WordPress GitHub repository](https://github.com/wordpress/wordpress) has been cloned in `~/Development/wordpress/`.

Notes:
* It may be worthwhile to update the remote URL of the Platform repository to use SSH once it's set up so you don't have to enter your GitHub credentials every time you work with it, e.g.:
    * `cd ~/Development/vvv/www/wsuwp/`.
    * `git remote set-url`.
* the GitHub repository is a mirror of the WordPress subversion repository. Cloning from `git://core.git.wordpress.org/` instead may prove more reliable.

Platform deployments are managed with the [WSUWP Deployment plugin](https://github.com/washingtonstateuniversity/WSUWP-Deployment), which is activated on the Platform. More information about the deployment configuration is documented in that repository.

When a WordPress update is available, use the following steps (being sure to replace the example version numbers accordingly):

1. In a terminal window, navigate to your local copy of the WSUWP Platform repository with `cd ~/Development/vvv/www/wsuwp/`.
2. Check out a new branch with `git checkout -b wp496`.
3. Navigate to your local copy of the WordPress repository with `cd ~/Development/wordpress/`.
4. Fetch the latest tags from WordPress:
    * `git fetch --all`
    * `git fetch --tags`
    * `git tag` (or `git tag -l --sort=-v:refname` if you have trouble seeing the latest tag)
        * `q`you may need to exit with , depending on your application
5. Check out the latest tag with `git checkout 4.9.6`.
6. Sync WordPress to the Platform using `rsync --delete -rlgDh --exclude '.git' --exclude 'wp-content/plugins' --exclude 'wp-content/themes' ~/Development/wordpress/ ~/Development/vvv/www/wsuwp/www/wordpress/`.
7. Navigate back to the local copy of the Platform (`cd ~/Development/vvv/www/wsuwp/`).
8. Run `git status` to show the modified files. This is also a good time to check your development environment to ensure that the update was properly applied and that everything still operates as expected.
9. Commit the changes if everything looks good:
    * `git add -A`
    * `git commit -m "Update WordPress 4.9.6"`
10. Use a code editor to:
    1. update the version numbers of the Platform itself in the following files:
        * `package-lock.json`
        * `package.json`
        * `www/wp-content/mu-plugins/index.php`
    2. update the `$wsuwp_wp_changeset` number in `www/wp-content/mu-plugins/index.php`;
        * This number can be found after the `@` when the latest tag is checked out (step 5).
    3. Add a new entry in `CHANGELOG.md`.
11. Commit those changes, then push them to the remote repository:
    * `git add -A`
    * `git commit -m "Bump version 1.7.5"`
    * `git push origin wp496`
12. Visit the repository on GitHub and create a new pull request from the branch that was just pushed.
13. Merge the pull request into the master branch after the Travis CI check has passed.
14. Draft, then Publish a new release with the new Platform version number.

I like to switch back to the master branch in my local repositories, pull the changes, and delete the local branches I made once I've finished. This is all done through the terminal:
* `cd ~/Development/vvv/www/wsuwp/`
* `git checkout master`
* `git pull origin master`
* `git branch -d wp496`
and:
* `cd ~/Development/wordpress/`
* `git checkout master`
* `git pull origin master`