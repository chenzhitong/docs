# 智能合约示例——HelloWorld

```c#
<<<<<<< HEAD
public class HelloWorld : FunctionCode
=======
public class HelloWorld : SmartContract
>>>>>>> e5e43331cd35f87f336ded6b98df4277306e0359
{
    public static void Main()
    {
        Storage.Put(Storage.CurrentContext, "Hello", "World");
    }
}
```

<<<<<<< HEAD
Storage 类是操纵小蚁智能合约私有化存储区的静态类，通过 Storage.Put() 方法可以向私有化存储区中以 key-value 方式存储数据，详情可参考 [Storage类](../fw/dotnet/AntShares/Storage.md)。

完整代码请参考 [Github](https://github.com/AntShares/AntShares.SmartContract.Contracts)。 
=======
Storage 类是操纵 NEO 智能合约私有化存储区的静态类，通过 Storage.Put() 方法可以向私有化存储区中以 key-value 方式存储数据，详情可参考 [Storage 类](../fw/dotnet/neo/Storage.md)。
*原来的继承VerificationCode和FunctionCode现都改为继承SmartContract。

完整代码请参考 [Github](https://github.com/neo-project/examples)。 
>>>>>>> e5e43331cd35f87f336ded6b98df4277306e0359
