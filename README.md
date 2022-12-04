# ssl-and-tls-secret-kubernetes

## Self Signed Certificate

A self-signed SSL certificate is an SSL Certificate that is issued by the person creating it rather than a trusted certificate authority. This can be good for testing environments.

## Step 1: Generate a CA private key
```bash
openSSL genrsa -out ca.key 2048
```

## Step 2: Create a self-signed certificate, valid for 365 days
```bash
openssl req -x509 \
  -new -nodes  \
  -days 365 \
  -key ca.key \
  -out ca.crt \
  -subj "/CN=*.awsdevopstrainer.com"
```

## Step 3: Now, create the tls secret using the kubectl command or using the yaml definition
```bash
kubectl create secret tls nginx-tls-secret \
--key ca.key \
--cert ca.crt
secret "nginx-tls-secret" created
```
