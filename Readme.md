mv /home/quai/tempo-node/data /home/quai/tempo-node/data.bak-$(date +%Y%m%d-%H%M%S)
mkdir -p /home/quai/tempo-node/data

mkdir -p /home/quai/tempo-node/secrets

tempo consensus generate-private-key \
  --output /home/quai/tempo-node/secrets/validator_key.json

tempo consensus calculate-public-key \
  --private-key /home/quai/tempo-node/secrets/validator_key.json


tempo download --chain moderato --datadir /home/quai/tempo-node/data

tempo node \
  --datadir /home/quai/tempo-node/data \
  --chain moderato \
  --port 30303 \
  --discovery.addr 0.0.0.0 \
  --discovery.port 30303 \
  --consensus.signing-key /home/quai/tempo-node/secrets/validator_key.json \
  --consensus.fee-recipient 0x7b896407539587864401F92535cFa2b2f86bfaeD

  tempo node \
  --datadir /home/quai/tempo-node/data \
  --chain moderato \
  --port 30303 \
  --discovery.addr 0.0.0.0 \
  --discovery.port 30303 \
  --consensus.signing-key /home/quai/tempo-node/secrets/validator_key.json \
  --consensus.fee-recipient 0x7b896407539587864401F92535cFa2b2f86bfaeD \
  --http --http.addr 0.0.0.0 --http.port 8545 --http.api "eth,net,web3,txpool,trace" \
  --ws --ws.addr 127.0.0.1 --ws.port 8546 \
  --metrics 9000
