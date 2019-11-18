# openssl-how-to
Basic openssl commands

* Query a remote SSL Certificate

      /usr/bin/openssl s_client -showcerts -connect HOSTNAME:PORT -servername HOSTNAME
      /usr/bin/openssl verify -CAfile /path/to/cabundle.crt /path/to/server.crt
      /usr/bin/openssl ocsp -issuer /path/to/cabundle.crt -cert /path/to/server.crt -url http://ocsp.thawte.com -no_nonce
      /usr/bin/openssl x509 -text -noout -nameopt sep_semi_plus_space -in /path/to/server.crt

* Query a certificate (crt) file

      /usr/bin/openssl x509 -text -noout -nameopt sep_semi_plus_space -in /path/to/server.crt

* Query a certificate signing request (csr) file

      /usr/bin/openssl req -text -noout -verify -nameopt sep_semi_plus_space -in /path/to/server.csr

* Validate a certificate (crt) and its key (key) (md5 sums should match)

      /usr/bin/openssl x509 -noout -modulus -in /path/to/server.crt | /usr/bin/openssl md5
      /usr/bin/openssl rsa -noout -modulus -in /path/to/server.key | /usr/bin/openssl md5

* Validate a certificate sigining request (csr) and its key (key) (md5 sums should match)

      /usr/bin/openssl req -noout -modulus -in /path/to/server.csr | /usr/bin/openssl md5
      /usr/bin/openssl rsa -noout -modulus -in /path/to/server.key | /usr/bin/openssl md5

* Validate a certificate and its bundle/chain

      /usr/bin/openssl verify -CAfile /path/to/cabundle.crt /path/to/server.crt

* Generate a CSR

      /usr/bin/openssl genrsa -out /path/to/server.key 2048
      /usr/bin/openssl req -new -nodes -sha256 -config /path/to/server.cfg -key /path/to/server.key

* Generate a self-signed certificate

      /usr/bin/openssl genrsa -out /path/to/server.key 2048
      /usr/bin/openssl req -x509 -new -nodes -sha256 -days 3650 -config /path/to/server.cfg -key /path/to/server.key


