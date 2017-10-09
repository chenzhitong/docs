# ExecutionEngine class

<<<<<<< HEAD
The execution engine of the virtual machine can obtain the caller and execution container of the current contract

Namespace: [AntShares.SmartContract.Framework.Services.System](../System.md)

Assembly: AntShares.SmartContract.Framework

## syntax
=======
The execution engine of the virtual machine, allowing access to the caller and execution container.

Namespace: [Neo.SmartContract.Framework.Services.System](../System.md)

Assembly: Neo.SmartContract.Framework

## Syntax
>>>>>>> e5e43331cd35f87f336ded6b98df4277306e0359

```c#
public class ExecutionEngine
```

## Attributes

| | Name | description |
| ---------------------------------------- | ---------------------------------------- | -------------------------- |
<<<<<<< HEAD
([Https://i-msdn.sec.s-msft.com/dynimg/IC74937.jpeg] | [CallingScriptHash](ExecutionEngine/CallingScriptHash.md) | Get the script hash of the caller of the smart contract |
[EntryScriptHash](ExecutionEngine/EntryScriptHash.md) | Obtain the entry point for the smart contract (contract call chain). [Entry@html] The starting point of the script hash
[ExecutingScriptHash](ExecutionEngine/ExecutingScriptHash.md) | Get the script hash of the smart contract execution | |[][]() (https://i-msdn.sec.s-msft.com/dynimg/IC74937.jpeg)
[ScriptContainer](ExecutionEngine/ScriptContainer.md) | Get the script container for the smart contract (the first Triggers)
=======
| ![](https://i-msdn.sec.s-msft.com/dynimg/IC74937.jpeg) | [CallingScriptHash](ExecutionEngine/CallingScriptHash.md) | Returns the scripthash of the caller of the contract           |
| ![](https://i-msdn.sec.s-msft.com/dynimg/IC74937.jpeg) | [EntryScriptHash](ExecutionEngine/EntryScriptHash.md) | Returns the scripthash of the entry points of the contract(in the contract invocation chain) |
| ![](https://i-msdn.sec.s-msft.com/dynimg/IC74937.jpeg) | [ExecutingScriptHash](ExecutionEngine/ExecutingScriptHash.md) | Returns the scripthash of the executing contract             |
| ![](https://i-msdn.sec.s-msft.com/dynimg/IC74937.jpeg) | [ScriptContainer](ExecutionEngine/ScriptContainer.md) | Returns the script container of the current contract (The initial triggerer)      |
>>>>>>> e5e43331cd35f87f336ded6b98df4277306e0359
