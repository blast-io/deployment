# Deploying a Blast Node

This repo explains how to run a node for the [Blast](https://blast.io) L2 network. Blast is a fork of Optimism, so the deployment process is the same as that of a typical OP stack chain.

## Prereqs

1. Install [docker](https://docs.docker.com/engine/install/)

2. Copy the `.env.example` file to `.env` and set the values accordingly:

- NETWORK: `Blast network, value should be mainnet or sepolia`
- GETH_DATA_DIR: `Relative path to the directory that will store chain data`
- L1_RPC_URL: `Your L1 RPC endpoint`
- L1_RPC_KIND: `The type of RPC provider; valid options are: alchemy, quicknode, infura, parity, nethermind, debug_geth, erigon, basic, any`

## Running the node

```
docker compose up 

# if you want to run it in the background, use
# docker compose up -d
```

To test your node, you can run the following command to query the latest L2 block. Note that you will need to wait for your node to fully sync before this command will return the actual latest block.

```
curl -d '{"id":0,"jsonrpc":"2.0","method":"eth_getBlockByNumber","params":["latest",false]}' -H "Content-Type: application/json" http://localhost:9545
```

**To fully participate in p2p, please ensure TCP/UDP is allowed on port 9003, and add the argument `--p2p.advertise.ip=<host-machine-public-ip>` to the `op-node` service in the `docker-compose.yml` file.**

## Advanced usage

If you have custom deployment requirements, you may need to build the node software yourself. See [here](https://safe-violet-16b.notion.site/Blast-Testnet-Deployment-Docs-95c1882f41dc45a4aee62b01409b8516) for additional instructions.
