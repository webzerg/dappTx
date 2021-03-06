# dappTx


Visualizes transaction volume of biggest ethereum smart contracts. Pulls data from 
Infura, puts it in a postgres DB, (eventually a cron job). Exposed via a webapp 
that queries the DB, formats it properly for the front-end, which displays graphs. 

* hosted at: https://shrouded-journey-22394.herokuapp.com
* format: /api/:contractID/:startTime/:endTime (all three are in hex, grab these from etherscan)
* usage: https://shrouded-journey-22394.herokuapp.com/api/0x8d12a197cb00d4747a1fe03395095ce2a5cc6819/0x59bcb6cb/0x59c19f03

# important files

* pullData.js: hits the Infura API for all the transactions in the latest block and saves them to a local postgres DB. 
* frequency.js: returns contract tx frequency by timestamp
* server.js: entry point 

# get started locally

- npm install
- sudo -u postgres createdb tx
- psql -U postgres -d tx -f sql/makeTable.sql
- PGUSER='postgres' PGDATABASE='tx' PGPORT=5432 node pullData.js
- PGUSER='postgres' PGDATABASE='tx' PGPORT=5432 node server.js

# next

- build front end with chart.js. coinmarketcap.com for reference. @eswarasai helping here  

# future ideas

- scrape dapp contract names from etherscan?
- handle failed transactions. some blocks have tons https://etherscan.io/txs?block=4905182&p=1.
    to do this, explore transaction receipts trie https://github.com/ethereum/wiki/wiki/JSON-RPC#eth_getblockbyhash
- decentralized web stack? ipfs? 

inspirated by @owocki https://github.com/gitcoinco/skunkworks/issues/19#issuecomment-354695051
