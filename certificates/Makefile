
EASYRSA=/usr/share/easy-rsa

DOMAINS= gateway.festivalsapp.dev \
		identity-0.festivalsapp.dev \
		festivals-0.festivalsapp.dev \
		database-0.festivalsapp.dev \
		fileserver-0.festivalsapp.dev \
		website-0.festivalsapp.dev
		
SERVER_CERTS=$(patsubst %,%.crt,${DOMAINS})
CLIENT_CERTS=$(patsubst %,client.%.crt,${DOMAINS})


vpath %.crt pki/issued
	
certs: ${SERVER_CERTS} ${CLIENT_CERTS}

${CLIENT_CERTS}: 
	./easyrsa --passin=file:pwd --passout=file:pwd build-client-full $(subst .crt,,$@) nopass

${SERVER_CERTS}:
	./easyrsa --passin=file:pwd --passout=file:pwd build-server-full $(subst .crt,,$@) nopass

init: easyrsa pwd
	./easyrsa init-pki
	./easyrsa --passout=file:pwd --passin=file:pwd build-ca
	
easyrsa:
	sudo apt-get update && sudo apt-get -y install easy-rsa
	cp -r ${EASYRSA}/* .

pwd:
	echo 'insecure' > pwd
	


	