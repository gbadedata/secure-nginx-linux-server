# Implementation Notes

## Objective
The objective of this project was to deploy a small internet-facing Linux web server manually, apply baseline host hardening, configure Nginx, expose a static root page and a JSON endpoint, and secure the deployment with a valid SSL certificate.

## Process Summary
1. Provisioned an Ubuntu 24.04 EC2 instance on AWS
2. Created a DNS `A` record for the service subdomain
3. Installed Nginx, UFW, Certbot, and the Certbot Nginx plugin
4. Created and configured the `hngdevops` user
5. Added SSH public keys for administrative and checker access
6. Restricted passwordless sudo to only the required commands
7. Hardened SSH by disabling root login and password authentication
8. Configured UFW with only ports 22, 80, and 443 allowed
9. Configured Nginx to serve the root page and JSON API
10. Issued and deployed a Let's Encrypt certificate
11. Verified redirect, API response, certificate, renewal, firewall, and SSH behavior

## What Worked
- DNS resolution was correct before SSL issuance
- SSH key-based access worked for both the default Ubuntu user and `hngdevops`
- SSH hardening took effect without causing lockout
- UFW policy aligned with the intended attack surface
- Nginx served the required endpoints correctly
- Certbot successfully issued and deployed the certificate
- Certificate renewal dry-run succeeded

## What Did Not Work Smoothly
- Local PowerShell commands and remote Linux shell commands were initially mixed incorrectly
- The AWS `.pem` key and local `id_ed25519` key were stored in different paths, which created confusion
- The first version of the `/api` Nginx block produced a duplicate `Content-Type` header and had to be corrected
- Submission formatting required the bare domain instead of a full URL

## Key Lessons
- Separate local-machine tasks from server-side tasks clearly
- Validate SSH access before disabling password authentication
- Validate DNS before requesting certificates
- Keep security controls narrow and explicit
- Exact output formatting matters in systems that are automatically checked