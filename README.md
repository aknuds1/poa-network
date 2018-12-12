# POA Network

## How-To
POA Network is based on the Parity Ethereum client. In order to bootstrap a network,
go through the following steps:

1. Generate a password and set it as shell variable `PASSWORD`
2. Make an Ethereum key pair, entering your password from before when prompted: `mkdir -p parity/data parity/db && chmod -R a+w parity && docker run -ti --mount type=bind,source=$(pwd)/parity,target=/var/lib/parity parity/parity:beta -d /var/lib/parity/data --db-path /var/lib/parity/db account new`
