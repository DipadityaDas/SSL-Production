# SSL-Production
The best way to create valid SSL certificates for production environment.

## Self-Signed Certificate

### Step 1: Generate RSA

```code
openssl genrsa -aes256 -out ca-key.pem 4096
``` 

### Step 2: Generate a public CA Cert.

```code
openssl req -new -x509 -sha256 -days 3650 -key ca-key.pem -out ca.pem
```

### Step 3: Check the contains of the CA Cert.

```code
openssl x509 -in ca.pem -text
```

### Step 4: Generate rsa certificate key 

```code
openssl genrsa -out cert-key.pem 4096
```