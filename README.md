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

### Step 5: Create Certificate sign request

```code
openssl req -new -sha256 -subj "/CN=dipadityadas.me" -key cert-key.pem -out cert.csr
```

### Step 6: Create a file with subjectAltName

```code
echo "subjectAltName=DNS:*.dipadityadas.me,IP:65.0.183.123" >> extfile.cnf
```

### Step 7: Create the cert.pem file

```code
openssl x509 -req -sha256 -days 3650 -in cert.csr -CA ca.pem -CAkey ca-key.pem -out cert.pem -extfile extfile.cnf -CAcreateserial
```

### Step 8: Create fullchain certificate file

```code
cat cert.pem > fullchain.pem

cat ca.pem >> fullchain.pem
```

### Step 9: Add the CA file to RHEL 9 system

```code
cp ca.pem /etc/pki/ca-trust/source/anchors/ca.crt

update-ca-trust
```

