# Getblockhash method

<<<<<<< HEAD
Returns the hash value of the corresponding block based on the specified index.

## Parameter Description

Index: block index.

## Call the example
=======
Returns the hash value of the corresponding block, based on the specified index.

## Parameter Description

Index: Block index (block height)

## Example
>>>>>>> e5e43331cd35f87f336ded6b98df4277306e0359

Request text:

```json
{
<<<<<<< HEAD
   "Jsonrpc": "2.0",
   "Method": "getblockhash",
   "Params": [10000],
   "Id": 1
=======
   "jsonrpc": "2.0",
   "method": "getblockhash",
   "params": [10000],
   "id": 1
>>>>>>> e5e43331cd35f87f336ded6b98df4277306e0359
}
```

Response text:

```json
{
<<<<<<< HEAD
   "Jsonrpc": "2.0",
   "Id": 1,
   "Result": "4c1e879872344349067c3b1a30781eeb4f9040d3795db7922f513f6f9660b9b2"
=======
   "jsonrpc": "2.0",
   "id": 1,
   "result": "4c1e879872344349067c3b1a30781eeb4f9040d3795db7922f513f6f9660b9b2"
>>>>>>> e5e43331cd35f87f336ded6b98df4277306e0359
}
```