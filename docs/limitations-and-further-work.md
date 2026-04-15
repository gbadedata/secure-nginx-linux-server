# Limitations and Further Work

## Current Limitations
This deployment is intentionally small and manual. It solves the core server-hardening and secure-web-serving problem, but it has several limitations:

- No infrastructure as code was used
- No CI/CD pipeline was configured
- No configuration management or automated provisioning was used
- No monitoring or alerting stack was added
- No log aggregation or centralized observability was implemented
- No intrusion detection or host-based audit tooling was added
- DNS and certificate setup were tied to the single deployed instance
- The application layer is static and minimal
- There is no load balancing or multi-instance redundancy
- There is no secret management workflow beyond the baseline OS and Certbot setup

## Further Work
The following improvements would make the deployment more reusable and production-ready:

### 1. Infrastructure as Code
Rebuild the environment with Terraform or AWS CloudFormation so the full server, security group, and networking configuration can be recreated consistently.

### 2. Automated Provisioning
Use a bootstrap script or configuration management tool such as Ansible to automate user creation, SSH hardening, firewall rules, package installation, and Nginx deployment.

### 3. CI/CD
Add a GitHub Actions workflow to validate configuration files, test Nginx syntax, and optionally deploy approved changes to the server.

### 4. Monitoring and Logging
Integrate CloudWatch, Prometheus, Grafana, or another observability stack to monitor uptime, resource usage, certificate expiry, and service health.

### 5. Reverse Proxy and App Expansion
Extend the service beyond static content by deploying an application behind Nginx and introducing structured routing, upstream health checks, and service isolation.

### 6. Stronger Security Controls
Add fail2ban, auditd, log monitoring, least-privilege review, and regular security patch workflows.

### 7. High Availability
Move from a single-instance design to a more resilient architecture with an Application Load Balancer, autoscaling group, and DNS failover strategy if availability requirements increase.