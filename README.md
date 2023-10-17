### Running

1. `./init.sh` this will initialise the geth nodes with original genesis using 10s block time
2. Run bootnode using `./startBootnode.sh` in a seperate terminal
3. Run validator in a seperate terminal using `./startValidator1.sh`
4. Run non-validator node in a seperate terminal using `./startNode1.sh`
5. The validator node should now be sealing blocks every 10s and the non-validator node should be syncing the chain

### Testing to lower block time
1. In terminal running validator stop the geth process
2. Run `geth --datadir validator1 init genesis-low-block.json` to initalise the validator node with genesis for lower block period of 5s
3. Run validator again using `./startValidator1.sh`
4. Validator should now be producing blocks every 5s
5. In the terminal for node1 you will see an error similar to the following
```
ERROR[10-16|20:14:12.915] Failed to retrieve beacon bounds for bad block reporting err="beacon sync not yet started"
WARN [10-16|20:14:12.915] Synchronisation failed, dropping peer    peer=ed6cd60a1b266a026651b151b84f078b36de1b4a97ae1298b73c66ebd050ff18 err="retrieved hash chain is invalid: invalid timestamp"
```
6. Stop node1
7. Initialise the genesis of node1 to the lower blocktime using `geth --datadir node1 init genesis-low-block.json`
8. Start node1 again using `./startNode1.sh`
9. Node1 should be syncing again now

## Lowering block time seamlessly
Previous scenario shows that if block time configuration on node1 is shorter than on validator1 node,
node1 will fail to sync. Block time change may be smoother if on node 1 we'll set period low enough, or even lowest 
value, 1 second
1. Initialise the genesis of node1 to the lower blocktime using `geth --datadir node1 init genesis-low-block.json`
2. Initialise the genesis of validator1 to the lower blocktime using `geth --datadir validator1 init genesis.json`
3. Run bootnode using `./startBootnode.sh` in a seperate terminal
4. Run validator in a seperate terminal using `./startValidator1.sh`
5. Run non-validator node in a seperate terminal using `./startNode1.sh`
6. The validator node should now be sealing blocks every 10s and the non-validator node should be syncing the chain
### And to lower block time
1. In terminal running validator stop the geth process
2. Run `geth --datadir validator1 init genesis-low-block.json` to initalise the validator node with genesis for lower block period of 5s
3. Run validator again using `./startValidator1.sh`
4. Validator should now be producing blocks every 5s and the non-validator node should be syncing the chain without any 
additional actions taken on non-validator side