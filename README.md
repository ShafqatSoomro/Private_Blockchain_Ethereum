
# In this repository I will explain in detail that how to create Private Blockchain on Ethereum using puppeth.


# **Using Puppeth to create “Private Ethereum Blockchain” on Linux.**

### 1) Open command line terminal and creating working Directory/Folder for Blockchain.

	mkdir -p blockchain

### 2) Usign working Directory

	cd blockchain

### 3) This tool (puppeth) create a new Ethereum network down to  the genesis block, bootnodes, miners and eth stats servers without the hassle that it would normally entail.

	blockchain$ puppeth

### Please choose the following options from the (puppeth tool) for Ethereum Network. Here, I have listed down the options to choose one by one as they will be shown on screen.


*	Configure new genesis.
*	Ethash – proof-of-work.
* Creating new genesis from scratch.
* press Enter for Which account should be  
  pre-funded.
* Type yes for Should the pre-compiled address.
* Specify Chain/Network ID. Enter: 4224.
* Manage existing genesis.
* Export genesis configuration.
* Which folder so save the genesis specs into.
  Press Enter (for current folder)
* When comes on screen. What would like to do?
  (default = stats). Press ctrl+c for exiting.


### 4) Atom is a free and open-source text and source code editor for macOS, Linux, and Microsoft Windows with support for plug-ins written in JavaScript, and embedded Git Control.

 	blockchain$ atom

### atom editor will show the files of blockchain (folder).

### 5) Have a look into it and close the atom editor.

### 6) This command imports and sets the canonical genesis block for chain. geth(Go Ethereum) is a command line interface for running Ethereum node implemented in Go Language.

    	blockchain$ geth --datadir . init blockchain.json


### 7) Following command will create the account with password. (Please keep remember the password). Here, we will create 3 (three) accounts.

    	blockchain$ geth --datadir . account new

### 8) We can check accounts lists into keystore folder which is just created:

		blockchain$ ls keystore


### 9) Account lists with more information with geth command:

		blockchain$ geth --datadir . account list


### 10) Opening the atom editor and create a script file with the name of startnode.sh.  

		blockchain$ atom startnode.sh


### 11) Please type the following script as it is, on one line so that, it can execute/run without any issue and after that, save the file.


	geth --networkid 4224 --mine --miner.threads 2 --datadir "." --nodiscover --http --http.port "8545" --port "30303" --http.corsdomain "*" console --allow-insecure-unlock --nat "any" --http.api eth,web3,personal,net --unlock 0 --password ./password.txt --ipcpath "~/.ethereum/geth.ipc"


### 12) Here, we have to save the password in new file on atom editor as they have been asked on time of account creation. For example, password is abc123. So, create a new file on atom and name of the file is: password.txt and save that file.

### 13) Now, come into terminal window and change file mode. chmod +x on a file (script) only means, that we will make it executable.

		blockchain$ chmod +x startnode.sh


### 14) Now, run the file from current/blockchain directory.

		blockchain$ ./startnode.sh


### We may see that mining is started. Leave that terminal as it is and notice that blocks are creating.


### 15) Please open new command line terminal for attaching the node on console, if everything goes fine, node will be attached. And shows following message on screen.

### Welcome to the Geth JavaScript console!


	$ geth attach


### 16) Now, we may see the accounts with following command.

	> eth.accounts


### 17) Receiving the first account. (coinbase is the first account name)

	> eth.coinbase


### 18) Checking the balance of first account.

		> eth.getBalance(eth.coinbase)


### 19) We can get the ether balance with this command.

	> web3.fromWei(eth.getBalance(eth.coinbase), "ether")


### 20) We may also check the first account's balance with this command.

	> web3.fromWei(eth.getBalance(eth.accounts[0]), "ether")


### 21) Stop the mining.

	> miner.stop()


### 22) Start the mining.

	> miner.start(1)


### 23) For checking the Network ID.

	> net.version


### 24) We may unlock the accounts with password which have been used, as we saved in password.txt file. Unlock the second account.

	> personal.unlockAccount(eth.accounts[1], "abc123", 300)


###	Unlock the third account

	> personal.unlockAccount(eth.accounts[2], "abc123", 300)


### 25) Sending 10 ether from (coinbase/first account) to second account.


	> eth.sendTransaction({from: eth.coinbase, to: eth.accounts[1], value: web3.toWei(10, "ether")})


### Sending 20 ether from (coinbase/first account) to third account.

	> eth.sendTransaction({from: eth.coinbase, to: eth.accounts[2], value: web3.toWei(20, "ether")})


### 26) Now, we can check the balance of accounts.

### Account No. 2
	> web3.fromWei(eth.getBalance(eth.accounts[1]), "ether")

### Account No. 3
	> web3.fromWei(eth.getBalance(eth.accounts[2]), "ether")

### Press ctrl+D for exit/stop the blockchain.
