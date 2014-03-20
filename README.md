# Docker-ized bitcoind server

# Installation

#### Prerequisities

* grab some VPS (tested Digital Ocean with Ubuntu 13.10) - min 30GB disk, 2GB mem
* [install Docker](https://www.docker.io/gettingstarted/#h_installation)
* don't worry about losing containers, all esential data will be persistent in the main host filesystem
  * technically essential data folders will be mapped via docker volumes to `/var/lib/bitcoind-docker/*`

#### Installation

Following script will build and add a new container in your docker:

1. `binaryage/bitcoind` which is ([bitcoind](https://github.com/bitcoin/bitcoin) with mapped database to host's `/var/lib/bitcoind-docker/bitcoind`)

Steps:

    git clone git@github.com:binaryage/bitcoind-docker.git
    cd bitcoind-docker
    touch .env
    echo "export BITCOIND_RPC_USER=some_user" >> .env
    echo "export BITCOIND_RPC_PASSWORD=some_password" >> .env
    ./do build
    ./do run

Note: Inspect etc/env and see more overrides you can add to your custom .env

##### Stop

    ./do stop

##### Start

    ./do start

##### Upgrade

    ./do stop
    git pull
    ./do build
    ./do rm
    ./do run

##### RPC

    ./do rpc getinfo

note: if you get error about connection to bitcoind, it may be that bitcoind is reindexing/parsing blockchaing at the beginning. Give it some time after you run/start the container.

## Credits

* Docker is awesome!
* Inspiration from [srid's discourse-docker](https://github.com/srid/discourse-docker)

[Licensed under MIT](LICENSE)