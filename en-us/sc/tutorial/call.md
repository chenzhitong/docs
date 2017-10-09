<<<<<<< HEAD
# Contract call

```c#
[AppCall]("XXXXXXXXXX") // ScriptHash
=======
# Contract Call

```c#
[AppCall("XXXXXXXXXX")] // ScriptHash
>>>>>>> e5e43331cd35f87f336ded6b98df4277306e0359
public static extern int AnotherContract (string arg);

public static void Main ()
{
<<<<<<< HEAD
     AnotherContract ("Hello");
}
```

In a smart contract, if you want to call other smart contracts that have been published to the chain chain, you can do this in this way. First add a declaration to the C # by AppCall and the script hash of the contract to be invoked. And then you can call it in the code.
=======
     AnotherContract ("Hello");
}
```

In a smart contract, you can use this to call other smart contracts that have been published to the chain. 
1. Add a declaration using AppCall and the script hash of the contract to be invoked.
2. Call it in the code.
>>>>>>> e5e43331cd35f87f336ded6b98df4277306e0359
