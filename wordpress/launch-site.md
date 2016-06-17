---
layout: page
title: Launch Sites on WSUWP
---

## Overview

## Move an existing stage site to production

1. [Request and deploy HTTPS](wsuwp-https.md) for the new domain.
1. Have everybody log out of the existing staging site.
1. [Search and replace](wp-cli/search-replace.md) the staging domain with the new domain.
1. Flush cache on the server.
1. Edit the site URL in the network admin.
1. [Request DNS](../general/dns-request.md) for the new domain.
1. Verify search engine visibility is set properly.
1. Verify analytics are configured.

## Add a new stage or production site

1. [Request and deploy HTTPS](wsuwp-https.md) for the new domain.
1. [Request DNS](../general/dns-request.md) for the new domain.
1. Add a new site on the appropriate network.
