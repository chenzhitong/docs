<<<<<<< HEAD
# System namespace

The System namespace is the API provided by the Smart Contract Execution Engine (AVM), which provides a way to access the execution environment of the smart contract.
=======
# System Namespace

The System namespace is the API provided by the Smart Contract Execution Engine (NeoVM), which provides a way to access the execution environment of the smart contract.
>>>>>>> e5e43331cd35f87f336ded6b98df4277306e0359

| API | Description |
| ---------------------------------------- | -------------------------- |
| System.ExecutionEngine.GetScriptContainer | Get the script container for this smart contract (the first trigger) |
<<<<<<< HEAD
| System.ExecutionEngine.GetExecutingScriptHash | Get the script hash of the smart contract execution |
| System.ExecutionEngine.GetCallingScriptHash | Get the script hash of the caller for this smart contract |
| System.ExecutionEngine.GetEntryScriptHash | Get the script hash of the entry point for the smart contract (the starting point of the contract call chain) |
=======
| System.ExecutionEngine.GetExecutingScriptHash | Get the scripthash of the executing smart contract  |
| System.ExecutionEngine.GetCallingScriptHash | Get the scripthash of the caller for this smart contract |
| System.ExecutionEngine.GetEntryScriptHash | Get the scripthash of the entry point for the smart contract (the starting point of the contract call chain) |

Note: The source code for the API above can be found under `Neo.VM` in the `src\Neo.VM\InteropService.cs` file.
>>>>>>> e5e43331cd35f87f336ded6b98df4277306e0359
