# Architecture

## Infrastructure
- Cloud provider: AWS EC2
- Operating system: Ubuntu Server 24.04 LTS
- Region: eu-central-1
- Instance type: t2.micro

## DNS
A public DNS `A` record was created so that `stage0.gbadedata.com` resolved to the EC2 public IPv4 address.

## Web Layer
Nginx was configured as the active web server and served:
- `/` as a static HTML page
- `/api` as a JSON endpoint

## Security Controls
- Non-root user `hngdevops`
- Root SSH login disabled
- Password-based SSH authentication disabled
- Key-based SSH access enabled
- UFW enabled
- Only ports 22, 80, and 443 exposed

## TLS
A Let's Encrypt certificate was issued and deployed with Certbot. HTTP traffic was redirected to HTTPS using a permanent `301` redirect.