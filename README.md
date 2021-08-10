# Unit18_Assignment_POA
by Mikhara Ramsing


These instructions are a guide for the employees of **ZBank** to experiment with a private testnet for the purposes of getting comfortable with blochain and in particular crypto currency. They explain what has been done to set up the private testnet **zbank** and how to interact with it.


## Creating and Sending crypto currency via MyCrypto Wallet (an already existing testnet)


If you would like to quickly see how to send and receive crypto, we can use an existing testnet via MyCrypto to get our first test of sending and receiving crypto.


	* Download MyCrypto (https://www.mycrypto.com/) and creat a new wallet on one of the Ethereum testnets (I picked Rinkeby).
		* ![image](1.MyCryptoWalletcreated)
	* To pre-load the wallet, go to (https://faucet.rinkeby.io/) and tweet request with your account address copied.
	* Click on Transaction History on MyCrypto to see request status
		* ![image](2.EthrequestedonRinkeby)
	* Refresh Account Balance to see ETH come through
		* ![image](3.EthloadedfromRinkebyinto wallet)
	* Share your Account address with colleagues to receive ETH
	* Paste your colleague's Account Address in "To" box in MyCrypto to send them ETH


## Creating **zbanknet** as a testnet to send/receive our own blockchain

These are the steps I followed to create the Zbank testnet. Please note the following tools must be downloaded in order to create the testnet:
	* [Go Ethereum](https://geth.ethereum.org/) 
	* MyCrypto from above

1. I opened Terminal on my Mac in the Blockchain tools and ran puppeth to create my genesis. **Use the proof of authority** consensus engine.
	* Proof of Authority - The Proof of Authority (PoA) algorithm is typically used for private blockchain networks as it requires pre-approval of, or voting in of, the account addresses that can approve transactions (seal blocks).
	* This is compared to the other option of proof of work - in which one party proves to others that a certain amount of a specific computational effort has been expended. Verifiers can subsequently confirm this expenditure with minimal effort on their part.

2. I then created accounts for two nodes for the network with a separate `datadir` for each using `geth`.
	* `./geth --datadir node1 account new'	
	* `./geth --datadir node2 account new'


3. Using `geth`, I then initialized each node with the zbanknet.json`.
        * `./geth --datadir node1 init zbanknet.json`
        * `./geth --datadir node2 init zbanknet.json'

        * Note the enode of node 1


4. Now the nodes can be used to begin mining blocks
	*  `./geth --datadir node1 --unlock "SEALER_ONE_ADDRESS" --mine --rpc --allow-insecure-unlock`
It should look like this if successfully mining:
![image](4.node1)

    *  `./geth --datadir node2 --unlock "SEALER_TWO_ADDRESS" --mine --port 30304 --bootnodes "enode://SEALER_ONE_ENODE_ADDRESS@127.0.0.1:30303" --ipcdisable --allow-insecure-unlock`
It should look like this if successfully mining:
![image](5.node2a)
![image](6.node2b)

5. Add your zbank testnet to your MyCrypto as a custom network using the Chain ID you set for your testnet and use 'ETH' for currency.

6. You can now send crypto from Node 1 to Node 2 on your the private ZBank testnet. Simply enter the public address of Node 2 whilst in your Node 1 wallet, select the amount of ETH and Send.

Node 1 Wallet looks like this:
![image](7.node1wallet)

Transaction from Node 1 Wallet to Node 2 Wallet looks like this:
![image](8. transaction from node1 to node2)

**Transaction successful!**
![image](9. transaction successful)