## Repro

Prepare account:

```sh
foundryup -n tempo
export TEMPO_RPC_URL=https://rpc.testnet.tempo.xyz
read ADDR PK < <(cast wallet new --json | jq -r '.[0] | "\(.address) \(.private_key)"')
cast rpc tempo_fundAddress "$ADDR" --rpc-url "$TEMPO_RPC_URL"
```

Next run multiple times until seeing flakiness:

```sh
forge script script/Mail.s.sol --private-key $PK --rpc-url $TEMPO_RPC_URL --broadcast
```

Should show:

```
[⠊] Compiling...
No files changed, compilation skipped
Script ran successfully.

## Setting up 1 EVM.

==========================

Chain 42429

Estimated gas price: 20.000172062 gwei

Estimated total gas used for script: 1149751

Estimated amount required: 0.022995217828456562 PathUSD

==========================

##### tempo-testnet
✅  [Success] Hash: 0x73312d429491fc4df46734b8aec07aa0c3a68ad15ba79670a5a41464c878fa42
Contract Address: 0x9Ce76FC43Ab217658dBc3893058eb2E951542694
Block: 5675835
Paid: 0.004546158220761696 PathUSD (454608 gas * 10.000172062 gwei)


##### tempo-testnet
✅  [Success] Hash: 0x6d6c2d9bc9732f39f05e66d963a5dadf2d9e993d9cba5ec2be494602c03c5aa3
Block: 5675835
Paid: 0.002139796817138512 PathUSD (213976 gas * 10.000172062 gwei)


##### tempo-testnet
❌  [Failed] Hash: 0xc03be7a6acfcf4ddebc4d87e160070e42bc3fa2c5b54af8ef0c07fb436a6a9dc
Block: 5675835
Paid: 0.000261624501486044 PathUSD (26162 gas * 10.000172062 gwei)


##### tempo-testnet
❌  [Failed] Hash: 0x7ea8ec0939086e53ec9986fa3a3d06d721c4d892ad6b8cbe5664936e98eec05b
Block: 5675835
Paid: 0.000237264082343012 PathUSD (23726 gas * 10.000172062 gwei)


##### tempo-testnet
✅  [Success] Hash: 0x84cc436e5a4f4c16624e17324d3eb680cd50bd86d7afeeb519306050cc49cbaf
Block: 5675835
Paid: 0.00025040430843248 PathUSD (25040 gas * 10.000172062 gwei)


Transactions saved to: /home/zerosnacks/Projects/work/repro_flaky_grantRole_transactions/broadcast/Mail.s.sol/42429/run-latest.json

Sensitive values saved to: /home/zerosnacks/Projects/work/repro_flaky_grantRole_transactions/cache/Mail.s.sol/42429/run-latest.json

Error: Transaction Failure: 0xc03be7a6acfcf4ddebc4d87e160070e42bc3fa2c5b54af8ef0c07fb436a6a9dc
Transaction Failure: 0x7ea8ec0939086e53ec9986fa3a3d06d721c4d892ad6b8cbe5664936e98eec05b
```
