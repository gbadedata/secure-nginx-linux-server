# Verification Checklist

The following checks were performed after deployment:

- DNS resolved correctly to the EC2 public IP
- Nginx was installed and active
- UFW was active
- Only ports 22, 80, and 443 were allowed
- Root SSH login was disabled
- Password SSH authentication was disabled
- `hngdevops` existed and had the required scoped sudo access
- The root endpoint `/` returned HTML with visible username text
- The `/api` endpoint returned HTTP 200 and the exact JSON payload
- The `/api` endpoint returned `Content-Type: application/json`
- HTTP redirected to HTTPS using status code 301
- The certificate issuer was Let's Encrypt
- Certbot renewal dry-run succeeded