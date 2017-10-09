# Getrawmempool method

<<<<<<< HEAD
Obtain an unrecognized transaction list in memory.

## Call the example
=======
Obtain the list of unconfirmed transactions in memory.

## Example
>>>>>>> e5e43331cd35f87f336ded6b98df4277306e0359

Request text:

```json
{
<<<<<<< HEAD
   "Jsonrpc": "2.0",
   "Method": "getrawmempool",
   "Params":[],
   "Id": 1
=======
   "jsonrpc": "2.0",
   "method": "getrawmempool",
   "params":[],
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
   "Result": [
     "B4534f6d4c17cda008a76a1968b7fa6256cd90ca448739eae8e828698ccc44e7"
   ]
}
```

These are the undetermined transactions received by the node, ie zero-confirmed transactions.
=======
   "jsonrpc": "2.0",
   "id": 1,
   "result": [
     "B4534f6d4c17cda008a76a1968b7fa6256cd90ca448739eae8e828698ccc44e7"
   ]
}
```

These are the unconfirmed transactions received by nodes, i.e. transactions with zero confirmations.
>>>>>>> e5e43331cd35f87f336ded6b98df4277306e0359
