This folder contains SSL material for the docker composition default FQDN.

This is how the certificate was created:
```
openssl req -new -newkey rsa:2048 -x509 -days 3650 -extensions v3_ca -keyout ca.pem -out ca.crt
openssl rsa -in ca.pem -out ca.key
openssl genrsa -out georchestra-dev.umrthema.univ-fcomte.fr.key 2048
openssl req -key georchestra-dev.umrthema.univ-fcomte.fr.key -new -out georchestra.mydomain.org.csr
openssl x509 -req -days 3650 -in georchestra-dev.umrthema.univ-fcomte.fr.csr -CA ca.crt -CAkey ca.key -CAcreateserial -out georchestra.mydomain.org.crt
```

For a public service, you should use Traefik's ability to [generate its own certificates](https://docs.traefik.io/user-guide/examples/#lets-encrypt-support) using [Let's Encrypt](https://letsencrypt.org/).
