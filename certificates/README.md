# Create certificates for the Festivals-App

To create the certificates you need to:
1. `make init` which will:
   * install easyrsa, 
   * create a password file with password 'insecure'
   * initialise the  easyrsa pki data structure
   * generate the certificate for the root CA

2. `make certs` which will:
   * create the SERVER and CLIENT certificates for the servers listed in DOMAINS

The certicates KEYs (including the CA key) are created in the `pki/private/` directory.

The signed CRTs are in the `pki/issued` directory, except for the root `ca.crt` which is in the `pki/` directory
