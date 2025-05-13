Only production environments need Trusted Certificate Authority (CA) certificates
You can get these from Digicert, Let's Encrypt, Godaddy, Cloudflare. Some offer free one's like Cloudflare, but use paid ones if production.
They have a short lifespan, and have to be renewed every 90 Days but can automate it.

Here is an example of an SSL certificate you would just use for one RD Gateway, this is not a wildcard SSL. Can be used for multiple RD Gateways if all the same FQDN![[Pasted image 20250418114714.png]]

This is a Wildcard SSL Certificate, you can use this with all your subdomains or other RD gateways. This supports multiple FQDN's
![[Pasted image 20250418115111.png]]