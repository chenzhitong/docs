<<<<<<< HEAD
# Network protocol

In the network structure, AntShares use point to point network structure, using TCP protocol for communication.

There are two kinds of node types in the network, namely, ordinary nodes and consensus nodes. Ordinary nodes can broadcast, receive and forward transactions, blocks, etc. Consensus nodes can create blocks. Refer to [this text](setup.md) for installation and deployment of nodes.

The agreement protocol of AntShares is very similar to Bitocin protocol, but they differ in terms of the data structure of the block, transaction and so on.

Agreement

### Byte order

All integer types in AntShares system are encoded using Little Endian, and only the IP address and port number are encoded using Big Endian.

### Hashing

Two different hash functions are used in the AntShares system: SHA256 and RIPEMD160. The former is used to generate longer hash values, while the latter is used to generate shorter hash values. Usually, generating the hash value of an object, will require the use two hash functions. For example, to generate a block or transaction hash, the SHA256 hash value has to be calcaluated twice. While generating a contract address, the first calculation be to calculate the script SHA256 hash, which is then followed by the calculation of the script RIPEMD160 hash.

In addition, the block will also use a hash tree (Merkle Tree) structure. The transcation hash of every action is combined and used in the calculation of another hash, where the above process is repeated until only one Root remains (Merkle Root).

### Variable type

Varint: Variable length integer, can be encoded according to the value of the expression to save space.

| Value | length | format |
| ------------- | ---- | ------------- |
| <0xfd | 1 | uint8 |
| <= 0xffff | 3 | 0xfd + uint16 |
| <= 0xffffffff | 5 | 0xfe + uint32 |
| 0xffffffff | 9 | 0xff + uint64 |

Varstr: Variable-length string consisting of a variable-length followed string. The string is encoded with UTF8.

| Size | field | data type | description |
| ------ | ------ | ------------- | ------------- |
| | Length | varint | The length of the string, in bytes
| Length | string | uint8 [length] | The string itself |

Array: An array of elements that consists of a variable length, followed by an element sequence.

### Fixed constants

The amount of money, price and other data in the AntShares system, the unified use of 64-bit fixed-point, the decimal precision of up to 10 <sup> -8 </ sup>, can be expressed in the range: [- 2 <sup> 63 </10 <sup> 8 </ sup>, +2 <sup> 63 </ sup>/10 <sup> 8 </ sup>]

Data structure
-------

### Blockchain

A blockchain is a logical structure that connects blocks in the form of unidirectional lists for storing transactions, assets, and so on.

### blocks

| Size | field | data type | description |
| - | ------------- | ------- | --------------------- |
| 4 | Version | uint32 | Block version, currently 0 |
| 32 | PrevBlock | uint256 | The hash value of the previous block |
| 32 | MerkleRoot | uint256 | The root of the transaction list
| 4 | Timestamp | uint32 | timestamp
| 4 | Index | uint32 | Block Height (Block Index) = Block Number - 1 |
ConsensusData | uint64 | Consensus Data (Consensus Node Generates Pseudorandom Number) |
| 20 | NextConsensus | uint160 | The hash value of the accounting contract for the next block
| 1 | - | uint8 | fixed to 1 |
Script | script | script used to verify the block
Transactions | tx[] | Transaction List |

When calculating the hash of the block, the entire block is not counted, but only the first seven fields of the header are used: Version, PrevBlock, MerkleRoot, Timestamp, Height, Nonce, NextMiner. Since MerkleRoot already contains the hash value for all transactions, any modification to the transaction also changes the hash value of the block.

The data structure of the block header is as follows:

| Size | field | data type | description |
| - | ------------- | ------- | --------------------- |
| 4 | Version | uint32 | block version, currently 0 |
| 32 | PrevBlock | uint256 | The hash value of the previous block |
| 32 | MerkleRoot | uint256 | The root of the transaction list
| 4 | Timestamp | uint32 | timestamp
| 4 | Index | uint32 | Block Height (Block Index) = Block Number - 1 |
ConsensusData | uint64 | Consensus Data (Consensus Node Generates Pseudorandom Number) |
| 20 | NextConsensus | uint160 | The hash value of the accounting contract for the next block
| 1 | - | uint8 | fixed to 1 |
Script | script | script used to verify the block
| 1 | - | uint8 | fixed to 0 |

The timestamp of each block must be later than the timestamp of the previous block. Generally, the timestamps of the two blocks differ by about 15 seconds, but there are exceptions to this rule. The height of the block must be equivalent to the height of the previous block, plus one.

### trade

| Size | field | data type | description |
| - | ---------- | --------- | ------------ |
| 1 | Type | uint8 | Transaction Type |
| 1 | Version | uint8 | Trading version, currently 0 |
| | | - | - | Data specific to transaction type
Attributes | tx_attr[] | Extra attributes of the transaction
| 34 *? | Inputs | tx_in[] | Input |
| 60 *? | Outputs | tx_out[] | Output |
Scripts | script[] | Scripts used to validate the transaction

All transactions in the AntShares system are recorded in transaction units. There are several types of transactions:

| Value | name | system cost | description |
| ---- | --------------------- | -------- | ---------------------- |
| 0x00 | MinerTransaction | 0 | Transactions for allocating byte fees |
| 0x01 | IssueTransaction | 500 \ | 0 | Transactions for Distributing Assets
| 0x02 | ClaimTransaction | 0 | Transactions for the distribution of AntShares coins
| 0x20 | EnrollmentTransaction | 1000 | (Not usable) Special transaction for registration as a consensus candidate |
| 0x40 | RegisterTransaction | 10000 \ | 0 | (Not usable) Transactions for asset registration
| 0x80 | ContractTransaction | 0 | Contract transaction, which is the most commonly used transaction type
| 0xd0 | PublishTransaction | 500 * n | (Not usuable) Special Transactions for Smart Contracts |
| 0xd1 | InvocationTransaction | 0 | Special transcations for calling smart contracts |

Each type of transaction has its own unique field in addition to the public field of the transaction. The exclusive fields for different types of transactions are described in detail below.

** MinerTransaction **

| Size | field | data type | description |
| ---- | ----- | ------ | ------- |
| | | | | | | Public fields for transactions
4 | Nonce | uint32 | Random number |
| | | | | | | Public fields for transactions

The first transaction for each block must be MinerTransaction. It is used to reward the book-keeper nodes with all the transaction fees in the current block.

The random number in the transaction is used to prevent hash conflicts.

** IssueTransaction **

There are no special fields for the asset issue transaction.

The asset manager can create an asset that has been registered in an asset chain and send it to any address through an asset issue transaction.

In particular, if the issue of assets is AntShares, then the deal will be free to send.

** ClaimTransaction **

| Size | field | data type | description |
| ---- | ------ | ------- | -------- |
| | | | | | | Public fields for transactions
34 * | | Claims | tx_in[] | For the distribution of AntShares shares
| | | | | | | Public fields for transactions

** EnrollmentTransaction **

> [!Warning]
Has been deactivated and replaced by the AntShares.Blockchain.RegisterValidator of the smart contract.

View [Alternative .NET Smart Contract Framework](../sc/fw/dotnet/AntShares/Blockchain/RegisterValidator.md)

View [Alternative Smart Contract API](../sc/api/AntShares.md)

** RegisterTransaction **

> [!Warning]
Has been deactived and replaced by AntShares.Blockchain.CreateAsset for the smart contract.

View [Alternative .NET Smart Contract Framework](../sc/fw/dotnet/AntShares/Blockchain/CreateAsset.md)

View [Alternative Smart Contract API](../sc/api/AntShares.md)

** ContractTransaction **

There is no special field for a contract transaction.

** PublishTransaction **

> [!Warning]
Has been deactivated and replaced by AntShares.Blockchain.CreateContract for the smart contract.

View [Alternative .NET Smart Contract Framework](../sc/fw/dotnet/AntShares/Blockchain/CreateContract.md)

View [Alternative Smart Contract API](../sc/api/AntShares.md)

** Invoking a Transaction **


| Size   | Field     | Data Type    | Description              |
| ---- | ------ | ------- | --------------- |
| -    | -      | -       | Public fields for transactions         |
| ?    | Script | uint8[] | Invoked by smart contract     |
| 8    | Gas    | int64   | Costs required to run the smart contract |
| -    | -      | -       | Publics fields for transactions         |


### Trading characteristics

| Size | field | data type | description |
| ------ | ------ | ------------- | -------------- |
| 1 | Usage | uint8 | Use |
| 0 | | 1 | length | uint8 | data length (Omitted in certain cases)
| Length | Data | uint8 [length] | Application-specific external data |

Occasionally, the transaction will need to contain some data for external use. This data will be placed in the transaction characteristics of the field.

Each transaction feature can have different uses:

| Value | name | description |
| --------- | --------------- | --------------- |
| 0x00 | ContractHash | Hash value of external contract
| 0x02-0x03 | ECDH02-ECDH03 | Public key for ECDH key exchange |
| 0x20 | Script | For additional verification of the transaction
| 0x30 | Vote | For voting
| 0x80 | CertUrl | Certificate Address |
| 0x81 | DescriptionUrl | External presentation information address |
| 0x90 | Description | Short introductory information |
| 0xa1-0xaf | Hash1-Hash15 | Used to store custom hash values ​​|
| 0xf0-0xff | Remark-Remark15 | Remarks |

For ContractHash, ECDH series, Vote, Hash, the data length is fixed to 32 bytes,and the length field is omitted;

For Script, you must explicitly give the data length, and the length can not exceed 65535;

For CertUrl, DescriptionUrl, Description, Remark, you must specify the length of the data, and the length can not exceed 255.

### Transaction input

| Size | field | data type | description |
| ---- | --------- | ------- | --------- |
| 32 | PrevHash | uint256 | Reference to the hash value of the transaction |
| 2 | PrevIndex | uint16 | Index that references the transaction output

### Transaction output

| Size | field | data type | description |
| ---- | ---------- | ------- | ---- |
| 32 | AssetId | uint256 | Asset Number |
8 | Value | int64 | Amount |
| 20 | ScriptHash | uint160 | Payment address |

Each transaction can only contain up to 65536 outputs.

### Verify the script

| Size | field | data type | description |
| ---- | ------------ | ------- | ------ |
| StackScript | uint8[] | Stack script code |
RedeemScript | uint8[] | Contract script code |

The stack script can only contain push operations instructions that are used to pass parameters (such as signatures) to contract scripts. The script interpreter will execute the stack script code first, and then, execute the contract script code.

In a transaction, the hash value of the contract script code must be consistent with the transaction output, which is part of the verification process. The process of script execution will be described in detail later.

Network message
-------

All network messages are sent through the following message structure:

| Size | field | data type | description |
| ------ | -------- | ------------- | ----------- |
| 4 | Magic | uint32 | Protocol identification number |
| 12 | Command | char [12] | Command |
| 4 | length | uint32 | Payload length |
4 | Checksum | uint32 | Checksum |
| Length | Payload | uint8 [length] | Message content |

Defined Magic value:

| Value | description |
| ---------- | ---- |
| 0x00746e41 | Official Website |
| 0x74746e41 | Test Network |

Command using utf8 encoding, length of 12 bytes, and fill the extra part using 0.

Checksum is the first 4 bytes of the Payload, which has undergone two SHA256 hash.

Payload varies depending on the order of the different formats, see below.

### Version

| Size | field | data type | description |
| - | ----------- | ------ | --------------- |
| 4 | Version | uint32 | Protocol version, currently 0 |
| 8 | Services | uint64 | The services provided by the node are currently 1 |
4 | Timestamp | uint32 | Current time |
| 2 | Port | uint16 | The port that is listening, or 0, if it is not listening
| 4 | Nonce | uint32 | Nodes for distinguishing the same public network
UserAgent | varstr | Client ID
| 4 | StartHeight | uint32 | Block Chain Height |
| 1 | Relay | bool | Whether to receive and forward

When a node receives a connection request, it immediately declares its version. There will be no other communication before both parties are aware of each other's version.

### Verack

Once the node receives the version message, it immediately responds to a verack as a reply.

There is no payload for this message.

## Getaddr

Requests a new list of active nodes, in order to increase the number of its own connections.

There is no payload for this message.

### Addr

| Size | field | data type | description |
| - | ----------- | ---------- | ---------- |
| 30 *? | AddressList | net_addr[] | Addresses of other nodes on the network |

After the node receives the getaddr message, it returns an addr message as a reply to provide information about the known node on the network.

### Getheaders

| Size | field | data type | description |
| ---- | --------- | --------- | ----------------- |
| 32 *? | HashStart | uint256[] | Node is known as the latest block hash
| 32 | HashStop | uint256 | Request the last block of the hash |

Requests a header package containing up to 2000 blocks with the number HashStart to HashStop to a node. To get the resulting block hash, you need to resend the getheaders message. This message is used to quickly download blockchain that does not contain related transactions.

### Headers

| Size | field | data type | description |
| ---- | ------- | -------- | ---- |
Headers | header[] | Block header |

After the node receives the getheaders message, it returns a headers message as the response, providing the requested block header.

### Getblocks

| Size | field | data type | description |
| ---- | --------- | --------- | ----------------- |
| 32 *? | HashStart | uint256[] | Node is known as the latest block hash
| 32 | HashStop | uint256 | Request the last block of the hash |

Requests a inv message containing a number from the HashStart to the HashStop block list to a node. If HashStart to HashStop block more than 500, then cut off at 500. To get the following block hash, you need to resend the getblocks message.

### Inv

| Size | field | data type | description |
| ---- | ------ | --------- | ---- |
| 1 | Type | uint8 | Listing Type |
| 32 *? | Hashes | uint256[] | list |

The node can broadcast the object information it owns, using this message. This message can be sent automatically, or it can be used to answer getblocks messages.

The list types are the following:

| Value | name | description |
| ---- | --------- | ---- |
| 0x01 | TX | Trading |
| 0x02 | Block | Block
| 0xe0 | Consensus | consensus data |

### Getdata

| Size | field | data type | description |
| ---- | ------ | --------- | ---- |
| 1 | Type | uint8 | Listing Type |
| 32 *? | Hashes | uint256[] | list |

Requests a specified object to a node, which usually sends an inv packet and filters out the known element.

### Block

| Size | field | data type | description |
| ---- | ----- | ----- | ---- |
Block | block | block |

Send a block to a node that responds to the getdata message of the requested data.

### Tx

| Size | field | data type | description |
| ---- | ----------- | ---- | ---- |
| ? | Transactions | tx | Transactions |

Send a transaction to a node to respond to the getdata message of the requested data.

| Size | field | data type | description |
| ---- | --------- | --------- | ----------------- |
| 32 *? | HashStart | uint256[] | node is known as the latest block hash |
| 32 | hashStop | uint256 | request the last block |
=======
# Network Protocol


NEO adopts a P2P network structure, in which nodes can communicate with each other through TCP/IP protocol. In this structure, there are two different types of nodes: peer nodes and validating nodes (referred to as Bookkeepers in the NEO Whitepaper). Peer nodes can broadcast, receive and transfer transactions or blocks, while validating node can create blocks.


The network protocol of NEO is roughly similar to bitcoin’s, however, data structures such as blocks or transactions are quite different.

Convention
----

1. Byte Order

    All integer types of NEO are Little Endian except for IP address and port number, these 2 are Big Endian.

1. Hash

   Two different hash functions are used in NEO: SHA256 and RIPEMD160. SHA256 is used to generate a long hash value, and RIPEMD160 is used to generate a short hash value. In general, we get an object's hash value by using hash function twice. For example, we use SHA256 twice when we want to generate block's or transaction's hash value. When generating a contract address, we will use SHA256 function first and then use RIPEMD160.

   In addition, the block will also use a hash structure called a Merkle Tree. It computes the hash of each transaction and combines one another then hash again, repeats this process until there is only one root hash (Merkle Root).

1. Variable Length Type

   + Variant: Variable length integer, can be encoded to save space according to the value typed.

      |Value|Length|Format|
      |---|---|---|
      |< 0xfd|1|uint8|
      |<= 0xffff|3|0xfd + uint16|
      |<= 0xffffffff|5|0xfe + uint32|
      |> 0xffffffff|9|0xff + uint64|

   + Varstr: Variable length string, consisting of variable length integer followed by strings. String encoded by UTF8.

      |Size|Field|DataType|Description|
      |---|---|---|---|
      |?|length|variant|The length of a string in bytes|
      |length|string|uint8[length]|string itself|

   + Array: The array consists of a variable length integer followed by a sequence of elements.

1. Fixed-point Number

   Data in NEO such as amount or price are 64 bit fixed-point number and the precision of decimal part is 10<sup>-8</sup>，range：[-2<sup>63</sup>/10<sup>8</sup>, +2<sup>63</sup>/10<sup>8</sup>)

Data Type
-------

1. Blockchain

   The blockchain is a kind of logical structure, which is connected in series with a one-way linked list. It is used to store the data of the whole network, such as transactions or assets.

1. Block

   |Size|Field|DataType|Description|
   |---|---|---|---|
   |4|Version|uint32|Version of the block which is 0 for now|
   |32|PrevBlock|uint256|Hash value of the previous block|
   |32|MerkleRoot|uint256|Root hash of a transaction list|
   |4|Timestamp|uint32|Time-stamp|
   |4|Height|uint32|Height of block|
   |8|Nonce|uint64|Random number|
   |20|NextMiner|uint160|Contract address of next miner|
   |1|-|uint8|It's fixed to 1|
   |?|Script|script|Script used to validate the block|
   |?*?|Transactions|tx[]|Transactions list|

   When calculating the hash value of the block, instead of calculating the entire block, only first seven fields in the block head will be calculated, which are version, PrevBlock, MerkleRoot, timestamp, and height, the nonce, NextMiner. Since MerkleRoot already contains the hash value of all transactions, the modification of transaction will influence the hash value of the block.

   Data structure of block head:

   |Size|Field|DataType|Description|
   |---|---|---|---|
   |4|Version|uint32|Version of the block which is 0 for now|
   |32|PrevBlock|uint256|Hash value of the previous block|
   |32|MerkleRoot|uint256|Root hash of a transaction list|
   |4|Timestamp|uint32|Time-stamp|
   |4|Height|uint32|Height of block|
   |8|Nonce|uint64|Random number|
   |20|NextMiner|uint160|Contract address of next miner|
   |1|-|uint8|It's fixed to 1|
   |?|Script|script|Script used to validate the block|
   |1|-|uint8|It's fixed to 0|

   The time-stamp of each block must be later than previous block's time stamp. Generally the difference of two block's time stamp is about 15 seconds and imprecision is allowed. The height of the block must be exactly equal to the height of the previous block plus 1.

1. Transaction

   |Size|Field|DataType|Description|
   |---|---|---|---|
   |1|Type|uint8|Type of transaction|
   |1|Version|uint8|Trading version, currently 0|
   |?|-|-|Data specific to transaction types|
   |?*?|Attributes|tx_attr[]|Additional features that the transaction has|
   |34*?|Inputs|tx_in[]|Input|
   |60*?|Outputs|tx_out[]|Output|
   |?*?|Scripts|script[]|List of scripts used to validate the transaction|

   All processes in NEO system are recorded as transactions. There are several types of transactions:

   |Value|Name|System Fee|Description|
   |---|---|---|---|
   |0x00|MinerTransaction|0|Assign byte fees|
   |0x01|IssueTransaction|500\|0|Inssuance of asset|
   |0x02|ClaimTransaction|0|Assign GAS|
   |0x20|EnrollmentTransaction|1000|Enrollment for validator|
   |0x40|RegisterTransaction|10000|Assets register|
   |0x80|ContractTransaction|0|Contract transaction|
   |0xd0|PublishTransaction|500 * n|(Not usable) Special Transactions for Smart Contracts|
   |0xd1|InvocationTransaction|0|Special transactions for calling Smart Contracts|

   Each type of transaction, in addition to the public field, also has its own exclusive field. The following will describe these exclusive fields in detail.

   + MinerTransaction

      |Size|Field|DataType|Description|
      |---|---|---|---|
      |4|Nonce|uint32|random number|

      The first transaction in each block must be MinerTransaction. It is used to reward all transaction fees of the current block to the validator.

      Random number in the transaction is used to avoid hash collision.

   + IssueTransaction

      There are no special fields for an issue transaction.

      Asset managers can create the assets that have been registered in NEO's block chain through IssueTransaction, and sent them to any address.

      In particular, if the assets which being issued are NEO, then the transaction will be sent free.

      Random number in the transaction is used to avoid hash collision.

   + ClaimTransaction

      |Size|Field|DataType|Description|
      |---|---|---|---|
      |34*?|Claims|tx_in[]|NEO for distribution|

   + EnrollmentTransaction

      |Size|Field|DataType|Description|
      |---|---|---|---|
      |33|PublicKey|ec_point|public key of validator|

      The transaction represents an enrollment form, which indicates that the sponsor of the transaction would like to sign up as a validator.

      The way to sign up is: To construct an EnrollmentTransaction type of transaction, and send a deposit to the address of the PublicKey.

      The way to cancel the registration is: Spend the deposit on the address of the PublicKey.

   + RegisterTransaction

      > [!Warning]
      Has been deactived and replaced by Neo.Asset.Create for the smart contract.

      View [Alternative .NET Smart Contract Framework](../sc/fw/dotnet/neo/Asset/Create.md)

      View [Alternative Smart Contract API](../sc/api/neo.md)

   + ContractTransaction

      There are no special attributes for a contract transaction. This is a very common kind of transaction as it allows one wallet to send NEO to another. The `inputs` and `outputs` transaction fields will usually be important for this transaction (for example, to govern how much NEO will be sent, and to what address).

   + PublishTransaction

      > [!Warning]
      Has been deactivated and replaced by Neo.Contract.Create for the smart contract.

      View [Alternative .NET Smart Contract Framework](../sc/fw/dotnet/neo/Contract/Create.md)

      View [Alternative Smart Contract API](../sc/api/neo.md)

   + Invoking a Transaction

      | Size   | Field     | Data Type    | Description              |
      | ---- | ------ | ------- | --------------- |
      | -    | -      | -       | Public fields for transactions         |
      | ?    | Script | uint8[] | Invoked by smart contract     |
      | 8    | Gas    | int64   | Costs required to run the smart contract |
      | -    | -      | -       | Publics fields for transactions         |

1. Transaction Attributes

   |Size|Field|DataType|Description|
   |---|---|---|---|
   |1|Usage|uint8|Usage|
   |0\|1|length|uint8|Length of data(Specific circumstances will be omitted)|
   |length|Data|uint8[length]|External data|

   Sometimes the transaction will contain some data for external use, these data will be placed in the transaction attributes field.

   Each transaction attribute has different usages:

   |Value|Name|Description|
   |---|---|---|
   |0x00|ContractHash|Hash value of contract|
   |0x02-0x03|ECDH02-ECDH03|Public key for ECDH key exchange|
   |0x20|Script|Additional validation of transactions|
   |0x30|Vote|For voting
   |0x80|CertUrl|Url address of certificate|
   |0x81|DescriptionUrl|Url address of description|
   |0x90|Description|Brief description|
   |0xa1-0xaf|Hash1-Hash15|Used to store custom hash values|
   |0xf0-0xff|Remark-Remark15|Remarks|

   For ContractHash, ECDH series, Hash series, data length is fixed to 32 bytes and length field is omitted;

   For CertUrl, DescriptionUrl, Description, Remark series, the data length must be clearly defined, and the length should not exceed 255;

1. Input of Transaction

   |Size|Field|DataType|Description|
   |---|---|---|---|
   |32|PrevHash|uint256|Previous transaction's hash|
   |2|PrevIndex|uint16|Previous transaction's index|

1. Output of Transaction

   |Size|Field|DataType|Description|
   |---|---|---|---|
   |32|AssetId|uint256|Asset id|
   |8|Value|int64|Value|
   |20|ScriptHash|uint160|Address of remittee|

   Each transaction can have outputs up to 65536.

1. Validation Script

   |Size|Field|DataType|Description|
   |---|---|---|---|
   |?|StackScript|uint8[]|Stack script code|
   |?|RedeemScript|uint8[]|Contract script code|

   Stack script can only be used for the PUSH operations, which is used to push data like signatures into the stack. The script interpreter will execute the stack script code first, and then execute the contract script code.

   In a transaction, the hash value of the contract script code must be consistent with the transaction output, which is part of the validation. The later section will describe the execution process of the script in detail.

Network Message
-------

All network messages are sent in this structure:

|Size|Field|DataType|Description|
|---|---|---|---|
|4|Magic|uint32|Protocol ID|
|12|Command|char[12]|Command|
|4|length|uint32|Length of payload|
|4|Checksum|uint32|Checksum|
|length|Payload|uint8[length]|Content of message|

Defined Magic value:

|Value|Description|
|---|---|
|0x00746e41|Production mode|
|0x74746e41|Test mode|

Command is utf8 code, of which the length is 12 bytes, the extra part is filled with 0.

Checksum is the first 4 bytes of the value that two times SHA256 hash of the Payload.

According to different orders Payload has different detailed format, see below:

1. version

   |Size|Field|DataType|Description|
   |---|---|---|---|
   |4|Version|uint32|Version of protocol, 0 for now|
   |8|Services|uint64|The service provided by the node is currently 1|
   |4|Timestamp|uint32|Current time|
   |2|Port|uint16|Port that the server is listening on, it's 0 if not used.|
   |4|Nonce|uint32|It's used to distinguish the node from public IP|
   |?|UserAgent|varstr|Client ID|
   |4|StartHeight|uint32|Height of block chain|
   |1|Relay|bool|Whether to receive and forward


   When a node receives a connection request, it declares its version immediately. There will be no other communication until both sides are getting versions of each other.

1. verack

   When a node receives the version message, it replies with a verack immediately.

   This message has no payload.

1. getaddr

   Make requests to a node for a batch of new active nodes in order to increase the number of connections.

   This message has no payload.

1. addr

   |Size|Field|DataType|Description|
   |---|---|---|---|
   |30*?|AddressList|net_addr[]|Other nodes' address in network|

   After receiving the getaddr message, the node returns an addr message as response and provides information about the known nodes on the network.

1. getheaders

   |Size|Field|DataType|Description|
   |---|---|---|---|
   |32*?|HashStart|uint256[]|Hash of latest block that node requests|
   |32|HashStop|uint256|Hash of last block that node requests|

   Make requests to a node for at most 2000 blocks’ header packages that contain HashStart to HashStop. To get the block hash after that, you need to resend the getheaders message. This message is used to quickly download the blockchain which does not contain the transactions.

1. headers

   |Size|Field|DataType|Description|
   |---|---|---|---|
   |?*?|Headers|header[]|Head of the block|

   After receiving the getheaders message, the node returns a header message as response and provides information about the known nodes on the network.

1. getblocks

   |Size|Field|DataType|Description|
   |---|---|---|---|
   |32*?|HashStart|uint256[]|Hash of latest block that node requests|
   |32|HashStop|uint256|Hash of last block that node requests|

   Make requests to a node for inv message which starts from HashStart to HashStop. The number of blocks which starts from HashStart to HashStop is up to 500. If you want to get block hash more than that, you need to resend getblocks message.

1. inv

   |Size|Field|DataType|Description|
   |---|---|---|---|
   |36*?|Inventories|inv_vect[]|Data of inventories|

   The node can broadcast the object information it owns by this message. The message can be sent automatically or can be used to answer getblocks messages.

   Object information is included in the list:

   |Size|Field|DataType|Description|
   |---|---|---|---|
   |4|Type|uint32|Type of object|
   |32|Hash|uint256|Hash of object|

   Object types:

   |Value|Name|Description|
   |---|---|---|
   |0x01|TX|Transaction|
   |0x02|Block|Block|
   |0xe0|Consensus|Consensus data|

1. getdata

   |Size|Field|DataType|Description|
   |---|---|---|---|
   |36*?|Inventories|inv_vect[]|Data of inventories|

   To request a specified object from a node: It is usually sent after the inv packet is received and the known element removed.

1. block

   |Size|Field|DataType|Description|
   |---|---|---|---|
   |?|Block|block|Block|

   Sending a block to a node, to respond to the getdata message.

1. tx

   |Size|Field|DataType|Description|
   |---|---|---|---|
   |?|Transaction|tx|Transaction|

   Sending a transaction to a node, to respond to the getdata message.

   |Size|field|data type|description|
   |----|---------|--------- |----------------- |
   |32 *?|HashStart|uint256[]|Node is known as the latest block hash|
   |32|hashStop|uint256|Request the last block|
>>>>>>> e5e43331cd35f87f336ded6b98df4277306e0359
