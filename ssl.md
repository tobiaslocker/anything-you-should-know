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

## Creating a certificate with certbot
```bash
# install
sudo apt-get update
sudo apt-get install software-properties-common
sudo add-apt-repository universe
sudo add-apt-repository ppa:certbot/certbot
sudo apt-get update
sudo apt-get install certbot python3-certbot-nginx

# create certificates
sudo certbot certonly --nginx
```

#### Use with [jwilder/nginx-proxy](https://github.com/nginx-proxy/nginx-proxy) and Docker Compose
In the directory containing `docker-compose.yml`
```console
$ mkdir certs
$ sudo cp /etc/letsencrypt/live/${MY_DOMAIN}/* ./certs
```

In `docker-compose.yml`s proxy service setting
```yaml
  reverseproxy:
    image: jwilder/nginx-proxy
    depends_on:
      - frontend
      - backend
    ports:
      - 80:80
      - 443:443
    volumes:
      - /var/run/docker.sock:/tmp/docker.sock
      - ./certs:/etc/nginx/certs
    environment:
      - "DEFAULT_HOST=decent.sh"
```

