# Rock-Scissors-Paper

## Explain code

这段代码是一个简单的猜拳游戏模块。它包含了一些结构体、常量和函数。

代码首先导入了一些标准库和自定义库，然后定义了一些常量和结构体。

在init函数中，创建了一个SuiHolder结构体对象，并将其共享给其他模块。

play函数是游戏的核心逻辑。它接受一个SuiHolder对象、玩家输入的手势、费用、时钟和交易上下文作为参数。

首先，代码检查费用是否足够支付游戏费用。如果不足，会抛出一个错误。

然后，代码从费用中扣除游戏费用，并将剩余的金额放入SuiHolder对象的余额中。

接下来，代码生成一个随机数来表示电脑的手势，然后根据随机数从一个包含所有手势的向量中取出电脑的手势。

代码生成一些日志信息，包括玩家输入的手势和电脑的手势，并将它们拼接在一起。

然后，代码根据玩家和电脑的手势判断游戏的结果，并生成相应的日志信息。

如果玩家和电脑出的手势相同，则是平局，代码会将游戏费用退还给玩家。

如果玩家输了，代码会生成相应的日志信息。

如果玩家赢了，代码会生成相应的日志信息，并将游戏费用的两倍退还给玩家。

最后，代码将结果通过事件发送出去。

总结：这段代码实现了一个简单的猜拳游戏模块，包括游戏逻辑、费用处理和结果生成。

这段代码是一个猜拳游戏的智能合约模块。以下是代码的步骤解释：

1. 引入所需的库和模块。
2. 定义了两个常量，ENotEnoughFee和EInCorretGestures，分别表示费用不足和手势错误的错误代码。
3. 定义了一个名为Result的结构体，包含一个字符串类型的msg字段。
4. 定义了一个名为SuiHolder的结构体，包含一个UID类型的id字段和一个`Balance<SUI>`类型的balance字段。
5. 定义了一个名为init的函数，接受一个TxContext类型的可变引用参数。在函数内部，创建了一个SuiHolder实例，并将其共享给其他模块。
6. 定义了一个名为play的公共函数，接受多个参数，包括一个可变引用的SuiHolder实例，一个u8类型的向量input_gesture，一个可变引用的`Coin<SUI>`实例fee，一个Clock实例clock和一个可变引用的TxContext实例ctx。
7. 在函数内部，首先检查传入的fee是否足够支付游戏费用，如果不足则抛出ENotEnoughFee错误。
8. 然后，根据游戏费用从fee中分割出支付金额，并将其转换为`Coin<SUI>`类型的实例pay_coin，并将其放入sui_holder的balance中。
9. 获取当前的时间戳，并计算出一个随机数random_num。
10. 创建一个空的向量all_gestures，并将三种手势（Rock、Scissors、Paper）依次添加到all_gestures中。
11. 根据random_num获取电脑选择的手势computer_gesture。
12. 创建两个字符串log1和log2，并将input_gesture和computer_gesture添加到log1和log2中。
13. 创建一个Result实例result1，将log2作为msg字段的值。
14. 发布result1事件。
15. 检查输入的手势是否正确，如果不正确则抛出EInCorretGestures错误。
16. 根据输入的手势和电脑选择的手势判断游戏结果，并将结果保存在变量log中。
17. 如果游戏是平局，则从sui_holder的balance中取回游戏费用并将其退还给发送者。
18. 如果游戏输了，则将log设置为"you lost!"。
19. 如果游戏赢了，则从sui_holder的balance中取回游戏费用的两倍并将其转账给发送者。
20. 创建一个Result实例result，将log作为msg字段的值。
21. 发布result事件。

## Build and Deploy contract

### Build

```bash
Code/sui/Rock-Scissors-Paper via 🅒 base 
➜ sui move build                 
UPDATING GIT DEPENDENCY https://github.com/MystenLabs/sui.git
INCLUDING DEPENDENCY Sui
INCLUDING DEPENDENCY MoveStdlib
BUILDING Rock-Scissors-Paper
Total number of linter warnings suppressed: 2 (filtered categories: 1)
```

### Deploy

```bash
Code/sui/Rock-Scissors-Paper via 🅒 base took 18.3s 
➜ sui client publish --gas-budget 100000000 --skip-fetch-latest-git-deps
[warn] Client/Server api version mismatch, client api version : 1.16.0, server api version : 1.15.0
INCLUDING DEPENDENCY Sui
INCLUDING DEPENDENCY MoveStdlib
BUILDING Rock-Scissors-Paper
Total number of linter warnings suppressed: 2 (filtered categories: 1)
Successfully verified dependencies on-chain against source.
Transaction Digest: D5nL7GoaHD2wLXggBGESPgNW4ciDfUcvA1RjqasnjgpX
╭─────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────╮
│ Transaction Data                                                                                                                                            │
├─────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────┤
│ Sender: 0x35370841d2e69b495b1e2f944a3087e4242f314e503691a00b054e0ee2a45a73                                                                                  │
│ Gas Owner: 0x35370841d2e69b495b1e2f944a3087e4242f314e503691a00b054e0ee2a45a73                                                                               │
│ Gas Budget: 100000000 MIST                                                                                                                                  │
│ Gas Price: 1000 MIST                                                                                                                                        │
│ Gas Payment:                                                                                                                                                │
│  ┌──                                                                                                                                                        │
│  │ ID: 0x3d1c101413a5668bfe8bdfcbfe871702e2198f0624b0d89d440aa9461943eb74                                                                                   │
│  │ Version: 12675223                                                                                                                                        │
│  │ Digest: CbiT8xUuFZGTkWqk6tGme4r9FCZYoTXEkfNKZbMYiQ6G                                                                                                     │
│  └──                                                                                                                                                        │
│                                                                                                                                                             │
│ Transaction Kind : Programmable                                                                                                                             │
│ Inputs: [Pure(SuiPureValue { value_type: Some(Address), value: "0x35370841d2e69b495b1e2f944a3087e4242f314e503691a00b054e0ee2a45a73" })]                     │
│ Commands: [                                                                                                                                                 │
│   Publish(<modules>,0x0000000000000000000000000000000000000000000000000000000000000001,0x0000000000000000000000000000000000000000000000000000000000000002), │
│   TransferObjects([Result(0)],Input(0)),                                                                                                                    │
│ ]                                                                                                                                                           │
│                                                                                                                                                             │
│                                                                                                                                                             │
│ Signatures:                                                                                                                                                 │
│    phdItMf3YMy6P1nuJ1w9nUrodO0q22fHDKY48PaEzUDuWX0/wZLIALuVTnO0rEp28TzYIET/h3MSXT3IHKHNAA==                                                                 │
│                                                                                                                                                             │
╰─────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────╯
╭───────────────────────────────────────────────────────────────────────────────────────────────────╮
│ Transaction Effects                                                                               │
├───────────────────────────────────────────────────────────────────────────────────────────────────┤
│ Digest: D5nL7GoaHD2wLXggBGESPgNW4ciDfUcvA1RjqasnjgpX                                              │
│ Status: Success                                                                                   │
│ Executed Epoch: 211                                                                               │
│                                                                                                   │
│ Created Objects:                                                                                  │
│  ┌──                                                                                              │
│  │ ID: 0x132b67a2e175b486f47a61a8566b8815b1086e634d1de72a240e4653a95000ab                         │
│  │ Owner: Immutable                                                                               │
│  │ Version: 1                                                                                     │
│  │ Digest: f1mpC5Up1Cw2Reb3Mv5RXfbiXDnx6BosgrvUgwkvJTX                                            │
│  └──                                                                                              │
│  ┌──                                                                                              │
│  │ ID: 0xaa38fb2f838a9bda199c292a8f523c99e13ec447c32018bf2df25666a2f66d85                         │
│  │ Owner: Account Address ( 0x35370841d2e69b495b1e2f944a3087e4242f314e503691a00b054e0ee2a45a73 )  │
│  │ Version: 12675224                                                                              │
│  │ Digest: 2VJy8EC8cMFVrLj5MkZ1MAQjn7WD4Y6wHPoVxxtANGuo                                           │
│  └──                                                                                              │
│  ┌──                                                                                              │
│  │ ID: 0xb59c5a296a44f2f14bbe69f759c7a7938f49676f30fc9a55e3ff7c9c11c8c8bb                         │
│  │ Owner: Shared                                                                                  │
│  │ Version: 12675224                                                                              │
│  │ Digest: 9C8KPFXSFG9bRyg7BJtaAeVvbswjjD5s4u98iziEXjia                                           │
│  └──                                                                                              │
│                                                                                                   │
│ Mutated Objects:                                                                                  │
│  ┌──                                                                                              │
│  │ ID: 0x3d1c101413a5668bfe8bdfcbfe871702e2198f0624b0d89d440aa9461943eb74                         │
│  │ Owner: Account Address ( 0x35370841d2e69b495b1e2f944a3087e4242f314e503691a00b054e0ee2a45a73 )  │
│  │ Version: 12675224                                                                              │
│  │ Digest: HcqMTiApK8hv4C9bQdESLS1VfkZTrxc2nx5s9QxMzpL9                                           │
│  └──                                                                                              │
│                                                                                                   │
│ Gas Object:                                                                                       │
│  ┌──                                                                                              │
│  │ ID: 0x3d1c101413a5668bfe8bdfcbfe871702e2198f0624b0d89d440aa9461943eb74                         │
│  │ Owner: Account Address ( 0x35370841d2e69b495b1e2f944a3087e4242f314e503691a00b054e0ee2a45a73 )  │
│  │ Version: 12675224                                                                              │
│  │ Digest: HcqMTiApK8hv4C9bQdESLS1VfkZTrxc2nx5s9QxMzpL9                                           │
│  └──                                                                                              │
│                                                                                                   │
│ Gas Cost Summary:                                                                                 │
│    Storage Cost: 17115200                                                                         │
│    Computation Cost: 1000000                                                                      │
│    Storage Rebate: 978120                                                                         │
│    Non-refundable Storage Fee: 9880                                                               │
│                                                                                                   │
│ Transaction Dependencies:                                                                         │
│    3pcBpJcaTZJstk5Ssu13zXjSaNQX2Xw1U2F66C9dajq5                                                   │
│    DQaT2XGjHarpU4DK9jCnEpZmzU9QqFyDXS4YKWYUQsNU                                                   │
│    HvsY1fCX5ueSnywNbfwMCEPo6Tuu3zw51bt5fyKbD4Hv                                                   │
╰───────────────────────────────────────────────────────────────────────────────────────────────────╯
╭─────────────────────────────╮
│ No transaction block events │
╰─────────────────────────────╯

╭────────────────────────────────────────────────────────────────────────────────────────────────────────────────╮
│ Object Changes                                                                                                 │
├────────────────────────────────────────────────────────────────────────────────────────────────────────────────┤
│                                                                                                                │
│ Created Objects:                                                                                               │
│  ┌──                                                                                                           │
│  │ ObjectID: 0xaa38fb2f838a9bda199c292a8f523c99e13ec447c32018bf2df25666a2f66d85                                │
│  │ Sender: 0x35370841d2e69b495b1e2f944a3087e4242f314e503691a00b054e0ee2a45a73                                  │
│  │ Owner: Account Address ( 0x35370841d2e69b495b1e2f944a3087e4242f314e503691a00b054e0ee2a45a73 )               │
│  │ ObjectType: 0x2::package::UpgradeCap                                                                        │
│  │ Version: 12675224                                                                                           │
│  │ Digest: 2VJy8EC8cMFVrLj5MkZ1MAQjn7WD4Y6wHPoVxxtANGuo                                                        │
│  └──                                                                                                           │
│  ┌──                                                                                                           │
│  │ ObjectID: 0xb59c5a296a44f2f14bbe69f759c7a7938f49676f30fc9a55e3ff7c9c11c8c8bb                                │
│  │ Sender: 0x35370841d2e69b495b1e2f944a3087e4242f314e503691a00b054e0ee2a45a73                                  │
│  │ Owner: Shared                                                                                               │
│  │ ObjectType: 0x132b67a2e175b486f47a61a8566b8815b1086e634d1de72a240e4653a95000ab::finger_guessing::SuiHolder  │
│  │ Version: 12675224                                                                                           │
│  │ Digest: 9C8KPFXSFG9bRyg7BJtaAeVvbswjjD5s4u98iziEXjia                                                        │
│  └──                                                                                                           │
│                                                                                                                │
│ Mutated Objects:                                                                                               │
│  ┌──                                                                                                           │
│  │ ObjectID: 0x3d1c101413a5668bfe8bdfcbfe871702e2198f0624b0d89d440aa9461943eb74                                │
│  │ Sender: 0x35370841d2e69b495b1e2f944a3087e4242f314e503691a00b054e0ee2a45a73                                  │
│  │ Owner: Account Address ( 0x35370841d2e69b495b1e2f944a3087e4242f314e503691a00b054e0ee2a45a73 )               │
│  │ ObjectType: 0x2::coin::Coin<0x2::sui::SUI>                                                                  │
│  │ Version: 12675224                                                                                           │
│  │ Digest: HcqMTiApK8hv4C9bQdESLS1VfkZTrxc2nx5s9QxMzpL9                                                        │
│  └──                                                                                                           │
│                                                                                                                │
│ Published Objects:                                                                                             │
│  ┌──                                                                                                           │
│  │ PackageID: 0x132b67a2e175b486f47a61a8566b8815b1086e634d1de72a240e4653a95000ab                               │
│  │ Version: 1                                                                                                  │
│  │ Digest: f1mpC5Up1Cw2Reb3Mv5RXfbiXDnx6BosgrvUgwkvJTX                                                         │
│  | Modules: finger_guessing                                                                                    │
│  └──                                                                                                           │
╰────────────────────────────────────────────────────────────────────────────────────────────────────────────────╯
╭───────────────────────────────────────────────────────────────────────────────────────────────────╮
│ Balance Changes                                                                                   │
├───────────────────────────────────────────────────────────────────────────────────────────────────┤
│  ┌──                                                                                              │
│  │ Owner: Account Address ( 0x35370841d2e69b495b1e2f944a3087e4242f314e503691a00b054e0ee2a45a73 )  │
│  │ CoinType: 0x2::sui::SUI                                                                        │
│  │ Amount: -17137080                                                                              │
│  └──                                                                                              │
│                                                                                                   │
╰───────────────────────────────────────────────────────────────────────────────────────────────────╯


Code/sui/Rock-Scissors-Paper via 🅒 base took 6.3s 
➜ sui client call --package 0x132b67a2e175b486f47a61a8566b8815b1086e634d1de72a240e4653a95000ab --module finger_guessing --function play --args 0xb59c5a296a44f2f14bbe69f759c7a7938f49676f30fc9a55e3ff7c9c11c8c8bb Scissors 0x3d1c101413a5668bfe8bdfcbfe871702e2198f0624b0d89d440aa9461943eb74 0x6 --gas-budget 10000000
[warn] Client/Server api version mismatch, client api version : 1.16.0, server api version : 1.15.0
Transaction Digest: DserJHKmHtJLCyJBtoyn8d2tiRARfs95nmfVpK7DcVbb
╭─────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────╮
│ Transaction Data                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    │
├─────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────┤
│ Sender: 0x35370841d2e69b495b1e2f944a3087e4242f314e503691a00b054e0ee2a45a73                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          │
│ Gas Owner: 0x35370841d2e69b495b1e2f944a3087e4242f314e503691a00b054e0ee2a45a73                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       │
│ Gas Budget: 10000000 MIST                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           │
│ Gas Price: 1000 MIST                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                │
│ Gas Payment:                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        │
│  ┌──                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                │
│  │ ID: 0x3fb5d73b96a9fcdfd9c30e952e1413e9615b76a9cfe9fa0d65d30e0289488f59                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           │
│  │ Version: 18123694                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                │
│  │ Digest: BpQwNfgDq5vejokkBuGMniJB5xu5R1TD11EjBRWnzkV7                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             │
│  └──                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                │
│                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     │
│ Transaction Kind : Programmable                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     │
│ Inputs: [Object(SharedObject { object_id: 0xb59c5a296a44f2f14bbe69f759c7a7938f49676f30fc9a55e3ff7c9c11c8c8bb, initial_shared_version: SequenceNumber(12675224), mutable: true }), Pure(SuiPureValue { value_type: Some(Vector(U8)), value: "Scissors" }), Object(ImmOrOwnedObject { object_id: 0x3d1c101413a5668bfe8bdfcbfe871702e2198f0624b0d89d440aa9461943eb74, version: SequenceNumber(18123694), digest: o#FGZwUAARySbxsEDMCkc6bC3r9Xc8bV3oA512ydNuCi46 }), Object(SharedObject { object_id: 0x0000000000000000000000000000000000000000000000000000000000000006, initial_shared_version: SequenceNumber(1), mutable: false })] │
│ Commands: [                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         │
│   MoveCall(0x132b67a2e175b486f47a61a8566b8815b1086e634d1de72a240e4653a95000ab::finger_guessing::play(Input(0),Input(1),Input(2),Input(3))),                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         │
│ ]                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   │
│                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     │
│                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     │
│ Signatures:                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         │
│    l639PbNlAa9reA9NQbtNNqw8eGDdijYfudH8edy1zOkPKxqd6ikBdRfmAaE0avJc6qzD+ZbNkQud3lESWgRQDw==                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         │
│                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     │
╰─────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────╯
╭───────────────────────────────────────────────────────────────────────────────────────────────────╮
│ Transaction Effects                                                                               │
├───────────────────────────────────────────────────────────────────────────────────────────────────┤
│ Digest: DserJHKmHtJLCyJBtoyn8d2tiRARfs95nmfVpK7DcVbb                                              │
│ Status: Success                                                                                   │
│ Executed Epoch: 211                                                                               │
│                                                                                                   │
│ Mutated Objects:                                                                                  │
│  ┌──                                                                                              │
│  │ ID: 0x3d1c101413a5668bfe8bdfcbfe871702e2198f0624b0d89d440aa9461943eb74                         │
│  │ Owner: Account Address ( 0x35370841d2e69b495b1e2f944a3087e4242f314e503691a00b054e0ee2a45a73 )  │
│  │ Version: 18128025                                                                              │
│  │ Digest: ByYLSPGGhnCeRwYebzEH1q7xK2WK6T3Hs1qMRooHuXdY                                           │
│  └──                                                                                              │
│  ┌──                                                                                              │
│  │ ID: 0x3fb5d73b96a9fcdfd9c30e952e1413e9615b76a9cfe9fa0d65d30e0289488f59                         │
│  │ Owner: Account Address ( 0x35370841d2e69b495b1e2f944a3087e4242f314e503691a00b054e0ee2a45a73 )  │
│  │ Version: 18128025                                                                              │
│  │ Digest: 938dHAaxT6F8R3fjCRLJU3KYb7RQerkBud1zkPQXFU4U                                           │
│  └──                                                                                              │
│  ┌──                                                                                              │
│  │ ID: 0xb59c5a296a44f2f14bbe69f759c7a7938f49676f30fc9a55e3ff7c9c11c8c8bb                         │
│  │ Owner: Shared                                                                                  │
│  │ Version: 18128025                                                                              │
│  │ Digest: npJrYtwM3tVPsGJZiCKELgSrVevYiXVcoK6tGyZrfhH                                            │
│  └──                                                                                              │
│                                                                                                   │
│ Shared Objects:                                                                                   │
│  ┌──                                                                                              │
│  │ ID: 0xb59c5a296a44f2f14bbe69f759c7a7938f49676f30fc9a55e3ff7c9c11c8c8bb                         │
│  │ Version: 18123694                                                                              │
│  │ Digest: CjnadJ2c1iwucuGsesfPq2R4aPg12TJCt8DtUskALxgr                                           │
│  └──                                                                                              │
│  ┌──                                                                                              │
│  │ ID: 0x0000000000000000000000000000000000000000000000000000000000000006                         │
│  │ Version: 18128024                                                                              │
│  │ Digest: FKDBD38UYqS3rcT8EMQqVBC9XWuYLyq7evbQKaksX53r                                           │
│  └──                                                                                              │
│                                                                                                   │
│ Gas Object:                                                                                       │
│  ┌──                                                                                              │
│  │ ID: 0x3fb5d73b96a9fcdfd9c30e952e1413e9615b76a9cfe9fa0d65d30e0289488f59                         │
│  │ Owner: Account Address ( 0x35370841d2e69b495b1e2f944a3087e4242f314e503691a00b054e0ee2a45a73 )  │
│  │ Version: 18128025                                                                              │
│  │ Digest: 938dHAaxT6F8R3fjCRLJU3KYb7RQerkBud1zkPQXFU4U                                           │
│  └──                                                                                              │
│                                                                                                   │
│ Gas Cost Summary:                                                                                 │
│    Storage Cost: 3412400                                                                          │
│    Computation Cost: 1000000                                                                      │
│    Storage Rebate: 3378276                                                                        │
│    Non-refundable Storage Fee: 34124                                                              │
│                                                                                                   │
│ Transaction Dependencies:                                                                         │
│    4YMesq99vj9Qo5v8ixD5hQoFmmQmmGzemCQSsVjFNGTC                                                   │
│    BpqVF1nsdQKsFRqvfaFzcWJvv5DeAoeMPLvY4xin7JJY                                                   │
│    D5nL7GoaHD2wLXggBGESPgNW4ciDfUcvA1RjqasnjgpX                                                   │
╰───────────────────────────────────────────────────────────────────────────────────────────────────╯
╭───────────────────────────────────────────────────────────────────────────────────────────────────────────╮
│ Transaction Block Events                                                                                  │
├───────────────────────────────────────────────────────────────────────────────────────────────────────────┤
│  ┌──                                                                                                      │
│  │ EventID: DserJHKmHtJLCyJBtoyn8d2tiRARfs95nmfVpK7DcVbb:0                                                │
│  │ PackageID: 0x132b67a2e175b486f47a61a8566b8815b1086e634d1de72a240e4653a95000ab                          │
│  │ Transaction Module: finger_guessing                                                                    │
│  │ Sender: 0x35370841d2e69b495b1e2f944a3087e4242f314e503691a00b054e0ee2a45a73                             │
│  │ EventType: 0x132b67a2e175b486f47a61a8566b8815b1086e634d1de72a240e4653a95000ab::finger_guessing::Result │
│  │ ParsedJSON:                                                                                            │
│  │   ┌─────┬──────────────────────────────────────────────────────────────┐                               │
│  │   │ msg │ computer's gesture is :Rock, your input_gesture is :Scissors │                               │
│  │   └─────┴──────────────────────────────────────────────────────────────┘                               │
│  └──                                                                                                      │
│  ┌──                                                                                                      │
│  │ EventID: DserJHKmHtJLCyJBtoyn8d2tiRARfs95nmfVpK7DcVbb:1                                                │
│  │ PackageID: 0x132b67a2e175b486f47a61a8566b8815b1086e634d1de72a240e4653a95000ab                          │
│  │ Transaction Module: finger_guessing                                                                    │
│  │ Sender: 0x35370841d2e69b495b1e2f944a3087e4242f314e503691a00b054e0ee2a45a73                             │
│  │ EventType: 0x132b67a2e175b486f47a61a8566b8815b1086e634d1de72a240e4653a95000ab::finger_guessing::Result │
│  │ ParsedJSON:                                                                                            │
│  │   ┌─────┬───────────┐                                                                                  │
│  │   │ msg │ you lost! │                                                                                  │
│  │   └─────┴───────────┘                                                                                  │
│  └──                                                                                                      │
╰───────────────────────────────────────────────────────────────────────────────────────────────────────────╯
╭────────────────────────────────────────────────────────────────────────────────────────────────────────────────╮
│ Object Changes                                                                                                 │
├────────────────────────────────────────────────────────────────────────────────────────────────────────────────┤
│                                                                                                                │
│ Mutated Objects:                                                                                               │
│  ┌──                                                                                                           │
│  │ ObjectID: 0x3d1c101413a5668bfe8bdfcbfe871702e2198f0624b0d89d440aa9461943eb74                                │
│  │ Sender: 0x35370841d2e69b495b1e2f944a3087e4242f314e503691a00b054e0ee2a45a73                                  │
│  │ Owner: Account Address ( 0x35370841d2e69b495b1e2f944a3087e4242f314e503691a00b054e0ee2a45a73 )               │
│  │ ObjectType: 0x2::coin::Coin<0x2::sui::SUI>                                                                  │
│  │ Version: 18128025                                                                                           │
│  │ Digest: ByYLSPGGhnCeRwYebzEH1q7xK2WK6T3Hs1qMRooHuXdY                                                        │
│  └──                                                                                                           │
│  ┌──                                                                                                           │
│  │ ObjectID: 0x3fb5d73b96a9fcdfd9c30e952e1413e9615b76a9cfe9fa0d65d30e0289488f59                                │
│  │ Sender: 0x35370841d2e69b495b1e2f944a3087e4242f314e503691a00b054e0ee2a45a73                                  │
│  │ Owner: Account Address ( 0x35370841d2e69b495b1e2f944a3087e4242f314e503691a00b054e0ee2a45a73 )               │
│  │ ObjectType: 0x2::coin::Coin<0x2::sui::SUI>                                                                  │
│  │ Version: 18128025                                                                                           │
│  │ Digest: 938dHAaxT6F8R3fjCRLJU3KYb7RQerkBud1zkPQXFU4U                                                        │
│  └──                                                                                                           │
│  ┌──                                                                                                           │
│  │ ObjectID: 0xb59c5a296a44f2f14bbe69f759c7a7938f49676f30fc9a55e3ff7c9c11c8c8bb                                │
│  │ Sender: 0x35370841d2e69b495b1e2f944a3087e4242f314e503691a00b054e0ee2a45a73                                  │
│  │ Owner: Shared                                                                                               │
│  │ ObjectType: 0x132b67a2e175b486f47a61a8566b8815b1086e634d1de72a240e4653a95000ab::finger_guessing::SuiHolder  │
│  │ Version: 18128025                                                                                           │
│  │ Digest: npJrYtwM3tVPsGJZiCKELgSrVevYiXVcoK6tGyZrfhH                                                         │
│  └──                                                                                                           │
╰────────────────────────────────────────────────────────────────────────────────────────────────────────────────╯
╭───────────────────────────────────────────────────────────────────────────────────────────────────╮
│ Balance Changes                                                                                   │
├───────────────────────────────────────────────────────────────────────────────────────────────────┤
│  ┌──                                                                                              │
│  │ Owner: Account Address ( 0x35370841d2e69b495b1e2f944a3087e4242f314e503691a00b054e0ee2a45a73 )  │
│  │ CoinType: 0x2::sui::SUI                                                                        │
│  │ Amount: -11034124                                                                              │
│  └──                                                                                              │
│                                                                                                   │
╰───────────────────────────────────────────────────────────────────────────────────────────────────╯

```

- <https://suiexplorer.com/object/0x132b67a2e175b486f47a61a8566b8815b1086e634d1de72a240e4653a95000ab?network=testnet>
