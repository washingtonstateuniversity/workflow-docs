---
layout: page
title: Search and Replace with WP-CLI
---

## Search and replace terms in content with WP-CLI

*Command*: `wp search-replace "original term" "replacement term" wp_table_name --dry-run`

### Move a site from one URL to another

The most common use of `wp search-replace` is to update URLs on a site when moving from `stage.site.wsu.edu` to `site.wsu.edu`.

First, determine the site's ID. This can be done through the site's network admin in a browser or also via WP-CLI.

* `wp site list` will show you a list of all sites.
* `wp site list | grep "site"` will show you a list of all sites that contain the term "site"

The ID of the site will be used to specify the targeted table names.

There are 4 variations that you will want to consider running. In the examples below, replace `9999` with the site ID.

* `wp search-replace "://stage.site.wsu.edu" "://site.wsu.edu" wp_9999_posts --dry-run`
* `wp search-replace "://stage.site.wsu.edu" "://site.wsu.edu" wp_9999_postmeta --dry-run`
* `wp search-replace ":\/\/stage.site.wsu.edu" ":\/\/site.wsu.edu" wp_9999_posts --dry-run`
* `wp search-replace ":\/\/stage.site.wsu.edu" ":\/\/site.wsu.edu" wp_9999_postmeta --dry-run`

The first two lines will catch most of the content. The second two lines target content that has been stored in a way which escapes slashes. If replacing content in a site with a path, the slashes are handled similarly.

* `wp search-replace ":\/\/stage.site.wsu.edu\/path" ":\/\/path.site.wsu.edu" wp_9999_posts --dry-run`

Note the `dry-run` at the end of each command. This allows you to test the command first to see how many results will replaced. Remove that from the line and the full query will run.

If you are moving many sites at once and they share similar paths, plan the commands out well in advance so that you replace URLs in the correct order.

Once content has been replaced, cache will need to be flushed to ensure a smooth transition.
