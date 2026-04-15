# Secure Nginx Linux Server

## Overview

This project documents the deployment of a secure Ubuntu-based web
server on AWS EC2 using Nginx, UFW, OpenSSH hardening, and Let's
Encrypt.

The deployment serves: - a static HTML page on `/` - a JSON API on
`/api`

It applies basic host-level hardening and exposes only the minimum
required network ports.

------------------------------------------------------------------------

## Objectives

The main objectives were to:

-   deploy a public Linux server
-   create a non-root administrative user
-   enforce key-based SSH access
-   disable root SSH login
-   disable password-based SSH authentication
-   restrict passwordless sudo to specific commands
-   allow only ports 22, 80, and 443 through the firewall
-   serve a static landing page and a JSON endpoint with Nginx
-   issue and deploy a valid Let's Encrypt certificate
-   enforce HTTP to HTTPS redirection

------------------------------------------------------------------------

## Stack

-   AWS EC2
-   Ubuntu Server 24.04 LTS
-   Nginx
-   UFW
-   OpenSSH
-   Certbot / Let's Encrypt

------------------------------------------------------------------------

## Endpoints

### Root

`/` serves a static HTML page that visibly includes the username `OJ`.

### API

`/api` returns:

``` json
{"message":"HNGI14 Stage 0","track":"DevOps","username":"OJ"}
```

------------------------------------------------------------------------

## Security Controls

The final deployed state included:

-   non-root user `hngdevops`
-   restricted passwordless sudo for:
    -   `/usr/sbin/sshd`
    -   `/usr/sbin/ufw`
-   `PermitRootLogin no`
-   `PasswordAuthentication no`
-   UFW enabled
-   only ports `22`, `80`, and `443` allowed
-   Nginx active as the web server
-   valid Let's Encrypt certificate installed
-   HTTP redirected permanently to HTTPS

------------------------------------------------------------------------

## Repository Structure

``` text
secure-nginx-linux-server/
├── README.md
├── .gitignore
├── docs/
├── configs/
└── screenshots/
```

------------------------------------------------------------------------

## Key Configuration Files

-   `configs/nginx-site.conf`
-   `configs/ssh-hardening.conf`
-   `configs/sudoers-hngdevops.txt`

------------------------------------------------------------------------

## Evidence

-   EC2 Instance
-   DNS Propagation
-   Package Installation Verification
-   Firewall Configuration
-   SSH Hardening
-   HTTP Validation Before SSL
-   Certificate Issue and Deployment
-   HTTP to HTTPS Redirect
-   HTTPS API Verification
-   Certbot Renewal
-   Certificate Issuer

------------------------------------------------------------------------

## Documentation

Additional details are in:

-   `docs/architecture.md`
-   `docs/implementation-notes.md`
-   `docs/limitations-and-further-work.md`
-   `docs/verification-checklist.md`

------------------------------------------------------------------------

## Limitations

This deployment is intentionally manual and single-node. It does not
include:

-   infrastructure as code
-   CI/CD pipelines
-   monitoring and alerting
-   centralized logging
-   high availability or redundancy

------------------------------------------------------------------------

## Further Work

Possible next steps include:

-   rebuilding the infrastructure with Terraform
-   automating provisioning with Ansible
-   adding CI/CD pipelines
-   integrating monitoring and log aggregation
-   extending the service behind Nginx (reverse proxy to app)
-   improving resilience with load balancing and autoscaling
