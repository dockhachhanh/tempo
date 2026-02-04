```bash
mv $HOME/tempo-node/data $HOME/tempo-node/data.bak-$(date +%Y%m%d-%H%M%S)
mkdir -p $HOME/tempo-node/data
```
```bash
mkdir -p $HOME/tempo-node/secrets
```
```bash
tempo consensus generate-private-key \
  --output $HOME/tempo-node/secrets/validator_key.json
```
```bash
tempo consensus calculate-public-key \
  --private-key $HOME/tempo-node/secrets/validator_key.json
```
```bash
tempo download --chain moderato --datadir $HOME/tempo-node/data
```
```bash
tempo node \
  --datadir $HOME/tempo-node/data \
  --chain moderato \
  --port 30303 \
  --discovery.addr 0.0.0.0 \
  --discovery.port 30303 \
  --consensus.signing-key $HOME/tempo-node/secrets/validator_key.json \
  --consensus.fee-recipient 0x7b8964075395878xxx
```
```bash
  tempo node \
  --datadir $HOME/tempo-node/data \
  --chain moderato \
  --port 30303 \
  --discovery.addr 0.0.0.0 \
  --discovery.port 30303 \
  --consensus.signing-key $HOME/tempo-node/secrets/validator_key.json \
  --consensus.fee-recipient 0x7b896407xxx \
  --http --http.addr 0.0.0.0 --http.port 8545 --http.api "eth,net,web3,txpool,trace" \
  --ws --ws.addr 127.0.0.1 --ws.port 8546 \
  --metrics 9000
```
