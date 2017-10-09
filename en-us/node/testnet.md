# Test network

<<<<<<< HEAD
The TestNet is designed to be developed, commissioned and tested by the user. Testing the system on the testnet incurs the network fee of testnet AntCoins (not real AntCoins)! Testnet AntShares and AntCoins can be applied for free of charge, on the official website.

All the block data of the test network is independent of the main network. If you develop a simple smart contract or try to register assets, the use of testnet should suffice. After the testing is complete, the development can be moved to the AntShares's mainnet online operation.

## Test the characteristics of the network

1. Asset registration, asset distribution, contract execution, etc. will not consume real money.
2. Globalized, deployed in the Internet environment.
3. Test the network block, transactions and other information can be easily viewed in the blockchain browser.
4. Smart contract deployed in the test environment, anyone around the world can employ it.
5. Test network can not be used as a commercial application of the actual landing environment.
=======
The TestNet is an environment where the user can develop, commission and test programs. Testing programs on the testnet incurs the network fee of testnet GAS (not real GAS!!). Testnet NEO and GAS can be applied free of charge, on the official website.

All the blockchain of the test network are independent of the main network. If you develop a simple smart contract or try to register assets, the use of testnet should suffice. After the testing is complete, the development can be moved to the NEO mainnet online operation.

If you are a developer, you can ask for GAS on the TestNet here: https://www.neo.org/Testnet/Create

## TestNet characteristics

1. Asset registration, asset distribution, contract execution, etc. (Does not consume real money)
2. Globalized deployment in the Internet environment.
3. Test of network blocks; Transactions and other information can be easily viewed in the blockchain browser.
4. Smart contract deployment in the test environment, where anyone in the world can employ it.
5. Test network can not be used as commercial application of an actual landing environment.
>>>>>>> e5e43331cd35f87f336ded6b98df4277306e0359

## Client Downloads

The test network client is the same as the primary network client. By modifying the client's configuration file, the client can be switched between the primary and test networks.

<<<<<<< HEAD
Reference: [introduction of AntShares node](introduction.md).

|      | AntSharesCore-GUI                        | AntSharesCore-CLI                        |
| ---- | ---------------------------------------- | ---------------------------------------- |
| Releases | [official website](https://www.antshares.org/download) or [Github](https://github.com/antshares/antsharescore/releases) | [Github](https://github.com/AntShares/antsharescore/releases) |
Source code | [Github](https://github.com/antshares/antsharescore) | [Github](https://github.com/antshares/antsharescore) |

## Method of switching to test network

1, Copy the contents of the program directory under the `protocal.testnet.json` into ` protocol.json`, as shown.

![image](http://docs.antshares.org/images/2017-06-08_14-16-35.png)

2, Copy the contents of the program (GUI) directory `AntSharesUI.exe.testnet.config` into the `AntSharesUI.exe.config`, as shown in Figure

![image](http://docs.antshares.org/images/2017-06-08_14-16-12.png)
=======
Reference: [Introduction of NEO node](introduction.md).

|      | Neo-GUI                        | Neo-CLI                        |
| ---- | ---------------------------------------- | ---------------------------------------- |
| Releases | [Official website](https://www.neo.org/download) or [Github](https://github.com/neo-project/neo-gui/releases) | [Github](https://github.com/neo-project/neo-cli/releases) |
| Source code | [Github](https://github.com/neo-project/neo-gui) | [Github](https://github.com/neo-project/neo-cli) |

## Method of switching to test network

1. Copy the contents of the program directory under the `protocal.testnet.json` into ` protocol.json` as shown.

![image](/assets/testnet_1.png)

2. Copy the contents of the program (GUI) directory `neo-gui.exe.testnet.config` into the `neo-gui.exe.config` as shown in Figure

![image](/assets/testnet_2.png)
>>>>>>> e5e43331cd35f87f336ded6b98df4277306e0359

Note: If the node is run on CLI, the contents of `config.testnet.json` need to be copied to` config.json`.
