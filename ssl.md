## Creating a self signed certificate

```bash
openssl req -x509 -new -nodes -key CA.key -sha256 -days 1024 -out CA.crt
openssl genrsa -out decent.sh.key 2048
# interactive
openssl req -new -key decent.sh.key -out decent.sh
openssl req -in decent.sh.csr -noout -text
openssl x509 -req -in decent.sh.csr -CA CA.crt -CAkey CA.key -CAcreateserial -out decent.sh.crt -days 500 -sha256
# verify
openssl x509 -in decent.sh.crt -text -noout
```
