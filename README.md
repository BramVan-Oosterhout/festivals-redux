# festivals-redux
An attempt to install Festivals-App from binaries in a docker container

This repository explores two activities needed to install the Festivals-App from the binaries:
1. certificates: generates the certificates for the application
2. festivals-backend-docker: install the binaries and configures the servers

Each directory contains a `Makefile` and a `README`

## Quick start
```
git clone git@github.com:BramVan-Oosterhout/festivals-redux.git 
cd festivals-redux/certificates/
make init certs
cd ../festivals-backend-docker/
make base build restart
```

