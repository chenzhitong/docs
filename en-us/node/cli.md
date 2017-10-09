# CLI Command Reference

<<<<<<< HEAD
Open the command line, navigate to the directory where the program is located, and enter the following code to start the command line wallet (ie, the AntShares node).

`dotnet AntSharesDaemon.dll`

This tutorial will introduce all the commands in the command line wallet. You can manipulate your wallet with commands for creating a wallet, importing and exporting of private key, transferring, starting a consensus, and so on.

We will first explore the various commands listed in the command line. In the command line, enter `help` followed by a carriage return, and you will see a list of orders as shown.

![image](http://docs.antshares.org/images/2017-05-17_12-30-05.jpg)

The following is a description of all the commands, the order of the brackets ``<> ```is the parameter, square brackets`[] `is optional parameters, and the symbol` | `displays the fill parameters can be any of any type, the equal sign `=` indicates the default value of the optional parameter without input.`
=======
Open the command line, navigate to the directory where the program is located, and enter the following code to start the command line wallet (ie the NEO node).

`dotnet neo-cli.dll`

This tutorial will introduce all the commands in the command line wallet. You can manipulate your wallet with commands for creating a wallet, importing and exporting of private key, transferring, starting consensus, etc.

We will first explore the various commands listed in the command line. In the command line, enter `help` followed by a return command, and you will see a list of commands as shown.

![image](/assets/cli_2.png)

The following is a description of all the commands and the order of the brackets:
Angular brackets ``<> `` indicate a parameter.
Square brackets`[]`is for optional parameters.
The symbol `|` displays the fill parameters, that can be any of any type.
The equal sign `=` indicates the default value of the optional parameter without an input.
>>>>>>> e5e43331cd35f87f336ded6b98df4277306e0359

## 1. Console Instructions

| Command      | Function Description      |
| ------- | --------- |
<<<<<<< HEAD
| version | shows the current software version |
| help    | help menu      |
| clear   | clear screen      |
| exit    | exit program      |
=======
| version | Shows the current software version |
| help    | Help menu      |
| clear   | Clear screen      |
| exit    | Exit program      |
>>>>>>> e5e43331cd35f87f336ded6b98df4277306e0359

## 2. Wallet operation

Command | Function Description | Remarks |
<<<<<<< HEAD
| ---------------------------------------- | -------- ------------------------ | ------ |
Create wallet \ <path> | create wallet file |
Open wallet \ <path> | open wallet file
Rebuild wallet index | need to open wallet
List all the accounts in the wallet | need to open the wallet
| List asset | list all assets in the wallet | need to open the wallet
List key | List all public keys in your wallet | Need to open wallet
Create address [n = 1] | create address/batch create address | need to open wallet |
| Import key \ <wif \ | path> | import private key/bulk import of private keys | need to open wallet |
Export key \ [address] [path] | export private key | need to open wallet |
Send to the specified address transfer parameters are: asset ID, the other party address, transfer amount, fee | need to open the wallet |

The following commands is explained in detail:

👉 `rebuild index`

Rebuild the wallet index. Why is it necessary to rebuild the wallet index?

There is a field in the wallet that records the height of the current wallet sync block. For each new one, the wallet client synchronizes the blocks and updates the assets and transactions in the wallet. Assuming that the currently recorded block height is 100, then you execute the import key command to import the private key, and the wallet still calculates your asset from the block height of 100. If the imported address has some transactions when the block height is less than 100, the transactions and the corresponding assets will not be reflected in the purse, so the wallet index should be rebuilt, forcing the wallet to calculate your assets from the block height of 0.
=======
| ---------------------------------------- | -------------------------------- | ------ |
| create wallet \<path> | Create wallet file |
| open wallet \<path> | Open wallet file |
| rebuild wallet index | | Need to open wallet |
| list all the accounts in the wallet | | Need to open wallet |
| list asset | List all assets in the wallet | Need to open wallet |
| list key | List all public keys in your wallet | Need to open wallet |
| create address [n = 1] | Create address / batch create address | Need to open wallet |
| import key \<wif\|path> | Import private key / bulk import of private keys | Need to open wallet |
| export key \[address] [path] | Export private key | Need to open wallet |
| send \<id\|alias> \<address> \<value> [fee=0]| Send to the specified address |Need to open wallet |

The following commands are explained in detail:

👉 `rebuild index`

This command is used to rebuild the wallet index.
Why is it necessary to rebuild the wallet index?

There is a field in the wallet that records the height of the current wallet sync block. For each new one, the wallet client synchronizes the blocks and updates the assets, and transactions in the wallet. Assuming that the current, recorded block height is 100, then you execute the import key command to import the private key, the wallet still calculates your asset from the block height of 100. If the imported address has some transactions when the block height is less than 100, the transactions and the corresponding assets will not be reflected in the wallet, so the wallet index should be rebuilt, forcing the wallet to calculate your assets from the block height of 0.
>>>>>>> e5e43331cd35f87f336ded6b98df4277306e0359

The newly created wallet does not need to rebuild the wallet index, only the imported private key is required to rebuild the wallet index.

👉 `create address [n = 1]`

<<<<<<< HEAD
You can enter create address to create a new address, you can also enter create address 100 to create 100 new addresses in batches; Batch creation of the address will be automatically exported to the address.txt file.

👉 `export key [address] [path]`

You can specify which addresses to export the corresponding private keys to. You can also specify the export to the specified file. (For example, the following command is legal) The command also requires the verification of the wallet password.
=======
This command can be used to create a new address. One can also enter 'create address 100' to create 100 new addresses in batches; Batch creation of the address will be automatically exported to the address.txt file.

👉 `export key [address] [path]`

You can specify which addresses to export the corresponding private keys to. You can also specify the export to the specified file. (See below for examples). The command also requires the verification of the wallet password.
>>>>>>> e5e43331cd35f87f336ded6b98df4277306e0359

Export key

Export key AeSHyuirtXbfZbFik6SiBW2BEj7GK3N62b

Export key key.txt

Export key AeSHyuirtXbfZbFik6SiBW2BEj7GK3N62b key.txt

👉 `import key <wif | path>`

<<<<<<< HEAD
When importing the private key, you can specify to import a private key, or import a file with a number of private keys. (The following order is legal)
=======
When importing the private key, you can specify to import a private key, or import a file with a number of private keys. (The following commands are legal)
>>>>>>> e5e43331cd35f87f336ded6b98df4277306e0359

Import key L4zRFphDJpLzXZzYrYKvUoz1LkhZprS5pTYywFqTJT2EcmWPPpPH

Import key key.txt

If there is a specified file, the file is in the private key format. Refer to export key key.txt output.

👉 `send <id | alias> <address> <value> [fee = 0]`

<<<<<<< HEAD
For transfers, there are a total of four parameters. The first parameter is the asset ID, the second parameter is the payment address, the third parameter is the transfer amount, and the fourth parameter is the fee (This parameter can be left empty, the default is 0) The command needs to verify the wallet password. For example, in order to transfer 100 antshares to the address "AeSHyuirtXbfZbFik6SiBW2BEj7GK3N62b", I would need to enter the following command.
=======
For transfers, there are a total of four parameters. The first parameter is the asset ID, the second parameter is the payment address, the third parameter is the transfer amount, and the fourth parameter is the fee. (This parameter can be left empty, and the default is 0) The command needs to verify the wallet password. For example, in order to transfer 100 NEO to the address "AeSHyuirtXbfZbFik6SiBW2BEj7GK3N62b", one would need to enter the following command.
>>>>>>> e5e43331cd35f87f336ded6b98df4277306e0359

Send c56f33fc6ecfcd0c225c4ab356fee59390af8560be0e930faebe74a6daff7c9b AeSHyuirtXbfZbFik6SiBW2BEj7GK3N62b 100

If you are not sure of the asset ID, please enter the list asset command to view all assets in the wallet.

## 3. View the node information

Command | Function Description |
| ---------- | ----------------------- |
<<<<<<< HEAD
Show state | Displays the current status of blockchain synchronization 
Show node | Displays the address and port of connected nodes |
Show pool | Display the transactions in the memory pool (These transactions are in the state of zero confirmation)
=======
show state | Displays the current status of blockchain synchronization
show node | Displays the address and port of connected nodes |
show pool | Display the transactions in the memory pool (These transactions are in the state of zero confirmation)
>>>>>>> e5e43331cd35f87f336ded6b98df4277306e0359
## 4. Advanced instructions

Command | Function Description |
| --------------- | ---- |
Start consensus | Begin consensus
<<<<<<< HEAD
Start the consensus on the premise that the wallet has a consensus authority, allows consensus authority to be obtained on the main net through voting. If a private chain is deployed, public key of the consensus can be set up in the `protocol.json`. Please refer to [Private chain](private-chain.md) for furher details.
=======
Start the consensus on the premise that the wallet has a consensus authority, allows consensus authority to be obtained on the main net through voting. If a private chain is deployed, public key of the consensus can be set up in the `protocol.json`. Please refer to [Private chain](private-chain.md) for further details.
>>>>>>> e5e43331cd35f87f336ded6b98df4277306e0359
