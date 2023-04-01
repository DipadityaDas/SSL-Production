# SSL-Production
The best way to create valid SSL certificates for production environment.

## Self-Signed Certificate

### Step 1: Generate RSA

```code
openssl genrsa -aes256 -out ca-key.pem 4096
``` 

### Step 2: Generate a public CA Cert
```code
openssl req -new -x509 -sha256 -days 365 -key ca-key.pem -out ca.pem

openssl x509 -in ca.pem -text
```

