---
layout: page
title: HTTPS on the WSUWP Platform
---

## Overview

### Generate a CSR

A CSR (Certificate Signing Request) is required in order to request a public key certificate from InCommon. This process is mostly automated and can be accessed under the main WSUWP network admin.

1. Go to the network admin dashboard at wp.wsu.edu.
1. Go to **Sites** and then **Manage Site TLS**
1. Enter a domain name in the **Generate a CSR** field and click **Get CSR**
1. The domain will appear in the list above. Click **View CSR**
1. Select the full text of the displayed CSR and copy it to your clipboard.

Be sure to copy the entire CSR, including `-----BEGIN CERTIFICATE REQUEST-----` and `-----END CERTIFICATE REQUEST-----`.

### Request a public key certificate from InCommon

Now that a CSR is available, it will be processed through InCommon to retrieve a public key certificate.

1. Open up the InCommon Certificate Manager [enrollment screen](https://cert-manager.com/customer/InCommon/ssl?action=enroll).
1. Enter the Access Code and Email address and click **Check Access Code** to login.
1. Enter the following on the SSL Enrollment screen:
	1. Access Code - this is the same as the one entered on the previous screen.
	1. Email - also the same as the one entered on the previous screen.
	1. Certificate Type
		1. **InCommon SSL (SHA-2)** if requesting a certificate that does not need a `www` subdomain.
		1. **InCommon Multi Domain SSL (SHA-2)** if requesting a certificate for a domain and its `www` subdomain.
	1. Certificate Term - 3 years.
	1. Server Software - Other.
	1. CSR - Paste the full text of the CSR generated in the previous steps.
	1. Common Name - Enter the domain used to generate the CSR. This will usually auto-populate once the CSR has been entered.
		1. If requesting a Multi Domain certicicate, a Subject Alternative Names input will appear. Enter the `www` subdomain in this field.
	1. Pass-phrase - Enter the pass-phrase.
	1. Comments - This is used to help parse the incoming email and route it accordingly. A comment will usually be in the form of `subdomain.wsu.edu, WSUWP Platform, nginx, sha-2` to include basic information about the request and where the certificate will be installed.
1. Click **Enroll**.

An email will appear shortly with an "Awaiting Approval" status. It may take several hours for an "Enrollment Successful" email to arrive containing the public key certificate.

### Upload a public key certificate to WSUWP

When the email arrives from InCommon with the certificate enrollment approval, there will be a series of links in the email to different versions of the public key certificate.

1. Click on the link labeled **as X509 Certificate only, Base64 encoded** to download the appropriate `.cer` file.
1. Go back to the **Manage Site TLS** screen from the first step.
1. Upload the certificate file using the **Upload Certificate** interface.

The status of the listed domain should now change from "View CSR" to "Awaiting Deployment". The server now has the private and public keys and has written a basic Nginx configuration for the domain.

### Deploy the certificate on the server

This is where the process becomes less automated. Files exist in a handful of directories on the server and need to be moved to their appropriate locations.

* `/home/www-data/to-deploy/` contains the private and public keys awaiting deployment.
* `/etc/nginx/ssl/` is where nginx expects to find these keys.
* `/home/www-data/deployed/` is where these keys will go after deployment.
* `/home/www-data/04_generated_config.conf` is the nginx configuration containing all generated domain configurations.
* `/etc/nginx/sites-enabled/` is where nginx expects to find this file.

The keys need to be copied to a new location, the generated nginx configuration needs to be moved, and the nginx server needs to be tested and reloaded.

1. SSH into the server.
2. Navigate with `cd /home/www-data/to-deploy/`.
3. List the files in the directory with `ls` and make sure these are domains that are ready to deploy.
4. Copy the files to the expected location with `cp /home/www-data/to-deploy/*.* /etc/nginx/ssl/`. If a notice comes up to overwrite an existing file, it is fine to say yes.
5. Move the files to their backup location with `mv /home/www-data/to-deploy/*.* /home/www-data/deployed/`.
6. Navigate a directory up with `cd /home/www-data/`.
7. Copy the generated nginx configuration with `cp /home/www-data/04_generated_config.conf /etc/nginx/sites-enabled/`. Choose yes to overwrite the existing file.
8. Test the nginx configuration with `sudo nginx -t`. See the below note before continuing.
9. Reload the nginx configuration with `sudo service nginx reload`.

#### A note on nginx configuration testing

You should see the following message after running `nginx -t`:

```
nginx: the configuration file /etc/nginx/nginx.conf syntax is ok
nginx: configuration file /etc/nginx/nginx.conf test is successful
```

If you do not see this message, then stop deployment and read the error carefully as it will usually explain the exact problem. Only continue deployment once `nginx -t` returns the expected lines above.

The certificate and domain configuration are now live. If it is not already, DNS for this domain should be pointed to the server.

### Verify certificate deployment

Once the certificate has been deployed and nginx has been reloaded, the **Manage Site TLS** screen will show a "Check Status" link next to the domain. This can be clicked to verify that an HTTPS connection is working. Once verified, click "Remove" to remove the domain name from the list.
