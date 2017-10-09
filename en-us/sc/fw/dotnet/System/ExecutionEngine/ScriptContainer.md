<<<<<<< HEAD
# ExecutionEngine.ScriptContainer property

The script container (the first trigger) of the smart contract is usually a transaction, and if the contract is triggered by the contract account transfer, the ScriptContainer is the transfer transaction if the contract is triggered by Invocation Transaction Then the ScriptContainer is the Invocation Transaction.

Namespace: [AntShares.SmartContract.Framework.Services.System](../../System.md)

Assembly: AntShares.SmartContract.Framework

## syntax

```c#
public extern AntShares.SmartContract.Framework.IScriptContainer ScriptContainer {get;}
```

Attribute value: script container, IScriptContainer type, if you know that it is a transaction triggered, you can turn it into [Transaction](../../AntShares/Transaction.md) type.



[Return to superior](../ExecutionEngine.md)
=======
# ExecutionEngine.ScriptContainer Property

Returns the script container of the current contract (The initial trigger). This is usually a transaction, if this contract was triggered by a transaction from a contract account, then the ScriptContainer will be of that transaction. If the current contract was trigger by an Invocation Transaction, then the ScriptContainer will be of that Invocation Transaction's.

Namespace: [Neo.SmartContract.Framework.Services.System](../../System.md)

Assembly: Neo.SmartContract.Framework

## Syntax

```c#
public extern Neo.SmartContract.Framework.IScriptContainer ScriptContainer {get;}
```

Attribute value: ScriptContainer as a IScriptContainer. If you know the trigger is a Transaction, you can cast this into a [Transaction](../../neo/Transaction.md).



[Back](../ExecutionEngine.md)
>>>>>>> e5e43331cd35f87f336ded6b98df4277306e0359
