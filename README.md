## container-problem-in-developer-node-arcium
this solve node-config.toml problem in arcium

## Replace your node-config.toml

```
nano node-config.toml
```

## Paste this config

```
[node]
rpc_url = "https://api.devnet.solana.com"
identity_keypair = "/usr/arx-node/node-keys/node_identity.pem"
operator_keypair = "/usr/arx-node/node-keys/node_keypair.json"
callback_keypair = "/usr/arx-node/node-keys/callback_keypair.json"
listen_address = "0.0.0.0:8000"
```

 ## SAVE 

 CTRL+O, ENTER, CTRL+X

## RUN THE NODE

```
nano run_arx_node.sh
```

## PASTE THIS 

```
#!/usr/bin/env bash
set -euo pipefail

CONTAINER="arx-node"
IMAGE="arcium/arx-node"

mkdir -p arx-node-logs

docker rm -f "$CONTAINER" 2>/dev/null || true

docker run -d --name "$CONTAINER" \
  -v "$(pwd)/node-config.toml:/usr/arx-node/node_config.toml" \
  -v "$(pwd)/node-keypair.json:/usr/arx-node/node-keys/node_keypair.json" \
  -v "$(pwd)/callback-kp.json:/usr/arx-node/node-keys/callback_keypair.json" \
  -v "$(pwd)/identity.pem:/usr/arx-node/node-keys/node_identity.pem" \
  -v "$(pwd)/arx-node-logs:/usr/arx-node/logs" \
  -p 8000:8000 \
  arcium/arx-node
```

## SAVE 

CTRL+O, ENTER, CTRL+X

## run code 

```
chmod +x run_arx_node.sh
./run_arx_node.sh
```

## View live logs

```
docker logs -f arx-node
```


## run this 

```
docker rm -f arx-node 2>/dev/null || true

docker run -d --name arx-node --pull always --restart unless-stopped \
  -v "$PWD/node-config.toml:/usr/arx-node/node_config.toml:ro" \
  -v "$PWD/node-keypair.json:/usr/arx-node/node-keys/node_keypair.json:ro" \
  -v "$PWD/callback-kp.json:/usr/arx-node/node-keys/callback_keypair.json:ro" \
  -v "$PWD/identity.pem:/usr/arx-node/node-keys/node_identity.pem:ro" \
  -v "$PWD/arx-node-logs:/usr/arx-node/logs" \
  -p 8000:8000 \
  arcium/arx-node
```



