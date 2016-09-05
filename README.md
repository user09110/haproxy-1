it's a haproxy.cfg file.

#####################################################################################
### Create a self-signed ssl-certificate:
openssl genrsa -out devdockerCA.key 2048
openssl req -x509 -new -nodes -key devdockerCA.key -days 10000 -out devdockerCA.crt
openssl genrsa -out domain.key 2048
openssl req -new -key domain.key -out dev-docker-registry.com.csr	###	DO NOT Set set password
openssl x509 -req -in dev-docker-registry.com.csr -CA devdockerCA.crt -CAkey devdockerCA.key -CAcreateserial -out domain.crt -days 10000
######################################################################################


#####################################################################################
### Install a self-signed ssl-certificate:
1) 	sudo mkdir /usr/local/share/ca-certificates/docker-dev-cert
2) 	sudo cp devdockerCA.crt /usr/local/share/ca-certificates/docker-dev-cert
3) 	sudo update-ca-certificates
#####################################################################################
