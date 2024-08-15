get: intermediate/db-install_node.sh intermediate/is-install.sh intermediate/fs-install.sh intermediate/fe-install.sh intermediate/gw-install.sh intermediate/insert_testdata.sql

mycert:
	cp ../certificates/pki/ca.crt intermediate/.
	cp ../certificates/pki/issued/*.crt intermediate/.
	cp ../certificates/pki/private/*.key intermediate/.

base: get
	docker build --progress=plain -f festivals.dck --tag my/festivals .

build: mycert

	docker build --progress=plain  -f configure.dck -t 'festivals-backend' .

run:
	docker rm -f festivals
	docker run  \
			   --name festivals \
			   --cap-add=SYS_PTRACE \
			   -d 'festivals-backend'
### --cap-add=NET_ADMIN for iptables

rebuild: build restart

restart: run
	docker exec -it festivals /bin/bash
			   
########### helpers
clean:
	-rm intermediate/*
intermediate/is-install.sh:
	curl -L -o is-intermediate/install.sh https://github.com/Festivals-App/festivals-identity-server/raw/master/operation/install.sh
intermediate/db-install.sh:
	curl -L -o intermediate/db-install.sh https://github.com/Festivals-App/festivals-database/raw/main/operation/install_database.sh
intermediate/db-install_node.sh: intermediate/db-install.sh
	curl -o intermediate/db-install_node.sh https://raw.githubusercontent.com/Festivals-App/festivals-database/main/operation/install_node.sh
intermediate/fs-install.sh:
	curl -L -o intermediate/fs-install.sh https://github.com/Festivals-App/festivals-fileserver/raw/master/operation/install.sh
intermediate/fe-install.sh:
	curl -o intermediate/fe-install.sh https://raw.githubusercontent.com/Festivals-App/festivals-server/main/operation/install.sh
intermediate/insert_testdata.sql:
	curl -L -o intermediate/insert_testdata.sql https://github.com/Festivals-App/festivals-database/raw/main/database_scripts/insert_testdata.sql