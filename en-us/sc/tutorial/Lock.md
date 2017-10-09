<<<<<<< HEAD
# Smart contract example - Lock (lock)
=======
# Smart Contract Example - Lock (Lock Contract)
>>>>>>> e5e43331cd35f87f336ded6b98df4277306e0359

```c#
public class Lock : FunctionCode
{
    public static bool Main(uint timestamp, byte[] pubkey, byte[] signature)
    {
        Header header = Blockchain.GetHeader(Blockchain.GetHeight());
<<<<<<< HEAD
        if (timestamp > header.Timestamp) return false;
=======
        if (header.Timestamp < timestamp)
            return false;
>>>>>>> e5e43331cd35f87f336ded6b98df4277306e0359
        return VerifySignature(pubkey, signature);
    }
}
```

<<<<<<< HEAD
The contract implements a function that specifies a timestamp that can not be fetched from the contract until the time of the blockchain system reaches the specified time, and when the blockchain system time After the specified time, the contract holder can take the funds out.

The current time is obtained in the code by the time of the latest block in the blockchain (the error is about 15 seconds). For details, refer to [Blockchain class](../fw/dotnet/AntShares/Blockchain.md), [Header class](../fw/dotnet/AntShares/Header.md).
=======
The contract implements a function that specifies a certain timestamp. Before the specified time stated, no one is allowed to withdraw any assets from the contract. Once the time stated is reached, the contract owners can then withdraw the assets.

The current time obtained by the contract is the time of the latest block in the blockchain (the error is about 15 seconds). For details, refer to [Blockchain class](../fw/dotnet/neo/Blockchain.md), [Header class](../fw/dotnet/neo/Header.md).

This contract inherits `FunctionCode`, thus it is meant to be deployed to the chain for others to call. If you wish to deploy a timelock contract locally, please refer to [Lock Contract](Lock2.md)
>>>>>>> e5e43331cd35f87f336ded6b98df4277306e0359
