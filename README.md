# openssl-how-to
Basic openssl commands

* Query a remote SSL Certificate and the certificate chain

      openssl s_client -showcerts -connect HOSTNAME:PORT -servername HOSTNAME </dev/null

* Display the contents of a remote SSL certificate

      openssl s_client -connect HOSTNAME:PORT </dev/null 2>/dev/null | openssl x509 -noout -text

* Display the contents of a local SSL certificate

      openssl x509 -text -noout -nameopt sep_semi_plus_space -in /path/to/server.crt

* Check to see if the certificate has been revoked

      openssl ocsp -issuer /path/to/cabundle.crt -cert /path/to/server.crt -url http://ocsp.thawte.com -no_nonce

* Query a certificate signing request (csr) file

      openssl req -text -noout -verify -nameopt sep_semi_plus_space -in /path/to/server.csr

* Validate a certificate (crt) and its key (key) (md5 sums should match)

      openssl x509 -noout -modulus -in /path/to/server.crt | openssl md5
      openssl rsa -noout -modulus -in /path/to/server.key | openssl md5

* Validate a certificate sigining request (csr) and its key (key) (md5 sums should match)

      openssl req -noout -modulus -in /path/to/server.csr | openssl md5
      openssl rsa -noout -modulus -in /path/to/server.key | openssl md5

* Validate a certificate and its bundle/chain

      openssl verify -CAfile /path/to/cabundle.crt /path/to/server.crt

* Generate a CSR

      openssl genrsa -out /path/to/server.key 2048
      openssl req -new -nodes -sha256 -config /path/to/server.cfg -key /path/to/server.key

* Generate a self-signed certificate

      openssl genrsa -out /path/to/server.key 2048
      openssl req -x509 -new -nodes -sha256 -days 3650 -config /path/to/server.cfg -key /path/to/server.key


* List all CA Certs installed on Centos server

      openssl crl2pkcs7 -nocrl -certfile /etc/ssl/certs/ca-bundle.crt | openssl pkcs7 -print_certs -text -noout|grep Subject:

# Various Notes

## MacOS: Sync CA Certificates from Keychain to Command Line Automatically

https://github.com/raggi/openssl-osx-ca#readme


