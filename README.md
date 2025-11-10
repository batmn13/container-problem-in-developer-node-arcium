## container-problem-in-developer-node-arcium
this solve container problem in arcium

## Create and save this script

Run this in your terminal

```
nano run_arx_node.sh
```

after that put this code 

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
  "$IMAGE"

docker exec -it "$CONTAINER" sh -c 'tail -F /usr/arx-node/logs/node.log'

```

## Save and exit

```
CTRL + O, ENTER, CTRL + X
```

## then run this
```
chmod +x run_arx_node.sh
```

## final step run this 

```
./run_arx_node.sh
```

your issue is solve gmpc
