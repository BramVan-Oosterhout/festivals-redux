# Creating athe docker image and running the container

## The Makefile
The docker image is built in two stages. 

The first stage creates an Ubuntu image (festivals) containing all required software and the servers as installed with the available `install.sh` scripts.

The second stage (configure) configures the installed servers and starts them

The Makefile is executed as follows:

1. `make base` will:
   * `get` the listed `install.sh` scripts from `github` and save them in the `intermediate` directory
   * build the `festivals` image as dexcribed in the `festivals.dck` dockerfile

2. `make build` will:
   * (mycerts target) copy the certificates generated in the `certificates` directory to the `intermediate` directory
    * because docker builds only from subordinate directories
   * build the `festivals-backend` image as described in the `configure.dck` file

3. `make run` will:
   * kill the running `festivals` container and remove it
   * start a container from the image `festivals-backend` and names it `festivals`

There are two pseudo targets included for convenience:
1. `make restart` will run the `festivals` container and starts a `bash` shell inside the container.

2. `make rebuild` will reconfigure the `festivals-backend` image, restart the `festivals` container and start the `bash` shell.

## The docker files

1. `festivals.dck` installs:
   * the ubuntu image as a starting point for the new image
   * ubuntu packages for required software, as well as some for development purposes
   * copies the desired `install.sh` scripts and executes them

2. `configure.dck` :
   * provides a shorthand ARG for the certificates available in the `intermediate` directory
   * add the root CA certificate to the containers certificate list
   * for each server:
      * copies the configuration file to `/etc/<server>.conf
      * copies the certificates to the configured locations
      * generates the required certificates in PEM format at the configured locations
   * sets up the container 
      * Note that docker cannot append `/etc/hosts`, but the container shell can. So that action occurs in entrypoint.sh
      