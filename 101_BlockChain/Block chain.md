## 

* bitcoin 借助 区块链 技术实现无信任中心的货币发行机制。
  * 交易账本 全网公开，可追溯，无法修改。

### 原理

每个区块包含一些列的记账信息，打包后形成一个区块 Block。

每个区块链接到前一个区块构成一个链 Chain。

每个完全节点拥有完成的区块链，**节点总是信任最长的区块链**。

#### **哈希方法**

1. **hash256**, 进行两次sha256
2. **hash160**， 先计算sha256，在计算RipeMD160



**Merkle Hash**

Merkle Hash 是所有交易信息的Hash。

如果有单数的交易信息，会对最后一个进行复制一个进行hash。

**如果修改任意一个记录，或者调换任意两个记录的顺序，都会使Merkle Hash变化。**

![image-20230112230607315](https://gitee.com/lynbz1018/image/raw/master/img/20230112230608.png)

**Block Hash**

是对区块头部进行hash 的值，如果区块被修改了，就能发现变化。

Prev Hash是对前一个区块的头部的Hash，可以向前找到前驱区块。

![image-20230112230516418](https://gitee.com/lynbz1018/image/raw/master/img/20230112230517.png)

**如果修改信息**

如果一个人修改了一个交易记录，Merkle Hash 需要重新计算，Block Hash也会变，后继区块指向前驱的也会断掉，需要重新计算后继的所有Prev Hash。

**所以随着时间的推移修改一个区块的难度会不断增加。一般经过6个区块后就基本可以认为无法再修改了。**



### P2P交易

去中心化，无需信任中介的点对点交易

使用数字签名技术，具有**不可伪造，不可篡改，不可抵赖**

使用的椭圆曲线签名算法，ECSDA签名

1. 私钥是一个256b的随机数
2. 公钥是私钥通过椭圆曲线算法生成的，一个私钥对应一个公钥

3. 使用私钥对交易信息hash加密，将签名 交易 公钥一起发出，接受者可以通过公钥解密签名得到hash 然后和收的交易信息hash后的值对比，一直即可确定正确并接受。

**私钥是唯一可以使用bitcoin的方法**，一旦丢失，公钥对应账户的财产就不能使用。

公钥是公开的，任何人都可以查询对应账户的余额，但是不知道账户是谁的，匿名特性。

<u>公钥是进行相互交易的，私钥是用于自己进行账户消费的。</u>



**比特币钱包** 是用于管理私钥的。



在实际交易中，输入会比输出大一点，这个差额就是隐含的交易费用，也就是矿工的记账收益。



#### 私钥

256位随机数 - 64个十六进制字符 - 32个字节

WIF (Wallet Import Format)



**非压缩的私钥**

`是否压缩说的是公钥，非压缩私钥会生成没有压缩的对应公钥，压缩私钥会生成对应的压缩的公钥`

37字节

1. 在32字节私钥前加0x80一个字节
2. 对33个字节进行两次SHA256，区前缀的4个字节作为校验码
3. 1字节0x80  32字节私钥 4字节校验码
4. 最后进行base58编码

![image-20230205165202896](https://gitee.com/lynbz1018/image/raw/master/img/20230205165204.png)

**压缩的私钥**

38字节

1. 在32字节前加0x80，后加0x01
2. 对34字节进行两次SHA256，取前缀4字节为校验码
3. 1字节0x80 32字节私钥 1字节0x01 4字节校验码
4. 进行base58编码

<img src="https://gitee.com/lynbz1018/image/raw/master/img/20230115165725.png" alt="image-20230115165724884" style="zoom:80%;" />



现在非压缩格式基本不使用了。

bitcoinjs提供的`ECPair`总是使用压缩格式的私钥表示

```javascript
const
	bitcoin = require('bitcoinjs-lib'),
    BigInteger = require('bigi');
let
	priv = '',
    d = BigInteger.fromBuffer(Buffer.from(priv, 'hex')),
    keyPair = new bitcoin.ECPair(d);

console.log(keyPair.toWIF());
```

`err: bitcoin.ECPair is not a constructor`

```javascript
const wif = require('wif');
let privateKey = '0c28fca386c7a227600b2fe50b7cae11ec86d3bf1fbe471be89827e19d72aa1d';
let encoded = wif.encode(
	0x80,
	Buffer.from(privateKey, 'hex'),
    true  // 压缩格式
);
console.log(encoded);
```

`nodejs中执行js文件`

`node ./test.js`

`npm install wif`



* 非压缩格式的WIF是以`5`开头
* 压缩格式的WIF是以`K`或`L`开头



#### 公钥

使用的是椭圆曲线数字签名ECDSA，根据私钥可以推导出两个256b的整数(x, y) 为非压缩格式的公钥

根据y的奇偶性在x的前面添加一个字节变成x' 为压缩格式的公钥

y为偶数是加0x02，为奇数时加0x03

<u>压缩格式和非压缩格式的公钥可以相互转换，但不能反向推导出私钥</u>

非压缩格式的公钥很少使用了, 使用非压缩格式的公钥脚本数据更长

```javascript
const bitcon = require('bitcoinjs-lib');
let
	wif = '',
    ecPair = bitccoin.ECPair.fromWIF(wif);
let pubKey = ecPair.getPublicKeyBuffer();
console.log(pubKey.toString('hex'));  // 获得的是02 或 03 开头的压缩格式的公钥
```



#### 地址

比特币的地址不是公钥，而是公钥的hash

25字节

1. 对33字节的压缩格式公钥Hash160
2. 添加前缀0x00
3. 对添加后的21字节，进行Hash256，取前四个字节作为校验码
4. 1字节0x00 20字节压缩公钥hash值 4字节校验码
5. 进行base58编码 以1开头的地址

![image-20230115192413503](https://gitee.com/lynbz1018/image/raw/master/img/20230115192414.png)

```javascript
const bitcoin = require('bitcoinjs-lib');
let 
	publicKey = '';
	ecPair = bitcoin.ECPair.fromPublicKeyBuffer(Buffer.from(publicKey, 'key'));

let addr = ecPair.getAddress();
console.log(addr);
```

是否压缩，公钥hash后得到的地址都是以1开头的地址

无法根据地址区分使用的是压缩格式还是非压缩格式公钥

以1开头的字符串，即为比特币收款地址，可以公开给任何人



#### 签名

用私钥对信息进行签名

```javascript
const bitcoin = require('bitcoinjs-lib');
let 
	message = 'balabal',
    hash = bicoin.crypto.sha256(message),
    wif = '',
    keyPair = bitcoin.ECPair.fromWIF(wif);

let signature = keyPair.sign(hash).toDER();

console.log('signature = ' + signarure.toString('hex'));
console.log('public key = ' + keyPair.getPublicKeyBuffer().toString('hex'));
```



获取信息 签名 公钥后，进行验证

```javascript
let signAsStr = '';
let 
	SignAsBuffer = Buffer.from(signAsStr, 'hex'),
    signatrure = bitcoin.ECSignature.fromDER(signAsBuffer),  // 获取签名的ECSignature对象
    message = 'balabal',
    hash = bitcoin.crypto.sha256(message),  // 对信息进行hash
    pubKeyAsStr = '',
    pubKeyAsBuffer = Buffer.from(pubKeyAsStr, 'hex'),
    pubKeyCheck = bitcoin.ECPair.fromPublickKeyBuffer(pubKeyAsBuffer);  // 创建公钥的ECPair

let res = pubKeyCheck.verify(hash, signature);
console.log('Verify resulet: ' + res);    
```



#### 挖矿原理

**带有经济激励的工作量证明**

**一个有效的工作量证明:** 计算需要用一定的时间, 但是验证过程很简单, 几乎可以瞬间完成

![image-20230205173106549](https://gitee.com/lynbz1018/image/raw/master/img/20230205173107.png)



通过不断变化`nonce`,计算Block Hash,直到找到比难度值低的Block Hash,就算挖矿成功.

难度值越小, 哈希值前面的0越多, 计算的难度越大.

比特币网络的难度是不断变化的, 要保证大约10分钟生产一个块.

难度在每2015个块之后进行调整. ` 比特币设计时本来打算每2016个区块调整一次难度，也就是两周一次，但是由于第一版代码的一个bug，实际调整周期是2015个区块。`

* 可以根据每个区块的**难度值**和**产出时间**, 推算出比特币网络的**全网算力**.
* 挖矿难度取决于全网算力的百分比, 比如有1%的全网算力, 每挖出100个区块, 你就有1个
* 确定一个新区块的hash值后, 向全网广播, 其他矿工进行验证, 通过后加入到区块链尾部, 该矿工在此次工作量证明中胜出, 其他矿工结束当前没有完成的区块, 开始下一个区块的工作量证明竞争

**安全传播**

Merkle Hash锁定了所有的交易信息, coinbase交易地址的第一个输出地址的该矿工地址, 每个矿工在挖矿时产生的数据都是不同的,所以不能窃取别人的工作量.

**共识算法**

两个矿工各自找到了有效区块, 这两这个区块不同

进行全网广播, 先收到哪个有效区块 就把哪一个进行验证后链接到区块链尾部   **所以进行了分叉**

但是最终总有一个分叉**先挖到后续区块**, 比特币网络采用**最长分叉**的共识算法, 短的分叉被废弃, 所有矿工又在最长的分叉上继续挖矿.



### 可编程支付原理

比特币的交易实际上不是直接支付到对方的地址上, 而是一个脚本: 即谁能提供另外一个脚本. 使这两个脚本能顺利执行通过, 谁就能花掉这笔钱.

比特币交易的输出是一个`锁定脚本` (只有这笔交易的接受者可以产生他对应的正确的解锁脚本, 也就是说他拥有这笔输出消费的权利), 下一个交易的输入是一个`解锁脚本`, 让锁定脚本正确运行, 那么该输入有效, 可以正常花掉这笔钱.

![image-20230205215000453](https://gitee.com/lynbz1018/image/raw/master/img/20230205215001.png)

`03开头的33位code 是压缩格式的公钥`

比特币脚本是一种基于**栈结构**的编程语言, 从第一行代码开始执行, 数据直接进行压栈.

`脚本执行完, 检查栈顶是否为0, 如果不为0, 那么整个脚本就执行成功了`



```markdown
小明支付给小红一笔比特币, 实际上是创建了一个锁定脚本, 脚本中引入小红的地址.
只有有正确的解锁脚本才能花出这笔钱
只有有对应私钥的小红才能创建正确的解锁脚本, 因为解锁脚本包含的签名只有用小红的私钥才能生成
所以小红事实上拥有了消费这笔钱的权利
```



* 比特币交易的本质是成功执行`锁定脚本`和`解锁脚本`, 所以可以编写任何符合条件的脚本.

* 多重签名: 让一笔交易在多数人同意的情况下才能够进行, 3个签名, 只要任意两个签名验证成功这笔交易就可以成功
  * 也一定程度上防止丢失私钥的风险, 3个人中如果由一个人丢失了私钥仍可以保证这笔消费是可以被花费的
* 比特币采用脚本的方式进行可编程支付：通过执行解锁脚本确认某个UTXO的资产可以被私钥持有人转移给其他人。





#### 多重签名

M-N多重签名, N个私钥中只要有任意M个私钥通过就可以使用资金.

多重签名降低了 因丢失私钥导致资金丢失 的风险.

```javascript
const bitcoin = require('bitcoinjs-lib');
let
    pubKey1 = '026477115981fe981a6918a6297d9803c4dc04f328f22041bedff886bbc2962e01',
    pubKey2 = '02c96db2302d19b43d4c69368babace7854cc84eb9e061cde51cfa77ca4a22b8b9',
    pubKey3 = '03c6103b3b83e4a24a0e33a4df246ef11772f9992663db0c35759a5e2ebf68d8e9',
    pubKeys = [pubKey1, pubKey2, pubKey3].map(s => Buffer.from(s, 'hex')); // 注意把string转换为Buffer

// 创建2-3 RedeemScript:
let redeemScript = bitcoin.script.multisig.output.encode(2, pubKeys);
console.log('Redeem script: ' + redeemScript.toString('hex'));

// 编码:
let scriptPubKey = bitcoin.script.scriptHash.output.encode(bitcoin.crypto.hash160(redeemScript));
let address = bitcoin.address.fromOutputScript(scriptPubKey);

console.log('Multisig address: ' + address); // 36NUkt6FWUi3LAWBqWRdDmdTWbt91Yvfu7
```

1. 设置好所有公钥列表 通过`bitcoin.script.multisig.output.encode()` 生成2-3类型的脚本
2. 对脚本进行HASH160, 再进行base58编码, 获得总以`3`开头的多重签名地址
   1. **以3开头的地址是多重签名地址**, 但不知道M/N中的M和N
3. ![image-20230207214036740](https://gitee.com/lynbz1018/image/raw/master/img/20230207214037.png)



* 多重签名地址并不知道使用的公钥(不知道使用的公钥就无法知道要使用哪些私钥), 而RedeemScript有使用的公钥信息和M/N数值, 所以想要花费多重签名地址的资金需要**M个私钥签名**和**RedeemScript**.
* 在线钱包使用2-3类型, 服务拥有一个, 用户拥有两个一个常规使用一个紧急使用.
  * 用户使用常规私钥可以完成交易, 且服务商一个私钥无法完成盗取
  * 如果服务商跑路或者被黑客攻击, 用户可以使用两个私钥进行资金转移
* 比特币最多允许15个私钥参与多重签名, 1-2 到 15-15的任意组合.



### UTXO 模型

UNspent TX Output: 没有被下一个交易花费的Output

每一个Input 连接前一个区块的 Output, 只有Coinbase(矿工奖励)没有Input.

所以每个Input都可以溯源到Coinbase交易.

![image-20230207221642060](https://gitee.com/lynbz1018/image/raw/master/img/20230207221643.png)

* 比特币中没有账户的概念, 想要确定某个人拥有的比特币, 就要计算这个人地址所关联的所有UTXO之和



**钱包程序**

钱包程序管理一组私钥, 对应一组公钥和地址

钱包程序从创世块开始扫描每一笔交易

1. 遇到某笔交易的Output, 对应地址钱包余额增加

2. 遇到某笔交易的Input, 对应地址的钱包余额减少

   `Input和Output看成是这个块的输入和输出, A地址关联的输入到块中A余额就减少了, B地址关联的从块中输出到B地址B的余额就增加了`

**钱包的当前余额总是 钱包地址关联的所有UTXO的金额之和.**



钱包程序从创世块开始扫描每一个区块,建立一个address-balance的数据映射表,用户查询余额时,从这个数据库通过索引查询.

一个区块记录后就不会再改变,所以这个数据库只用做增量更新即可.



### Segwit地址

* 隔离见证兼容地址

以3开头, 和多重签名地址不容易区分

兼容性好, 钱包程序不用修改, 可以直接付款到改地址



* Segwit隔离见证地址

都是以**bc**开头

1.公钥计算HASH160, 2.用**Bech32**编码, 3.用bc作为识别码并带校验码

中间用1连接

`bc 1 qmy63mjadtw8nhzl69ukdepwzsyvv4yex5qlmkd`

<img src="https://gitee.com/lynbz1018/image/raw/master/img/20230207230334.png" alt="image-20230207230333453" style="zoom: 80%;" />



ECDSA椭圆曲线签名会生成两个签名(r, s), 两个都有效, 且可以相互转换. 有风险**比特币延展性攻击**

延展性攻击, 黑客在交易发出但是没有落块时间内, 对签名进行修改(无法修改任何输入输出的地址和金额), 整个交易的哈希发生变化, 原始交易被丢弃, 虽然不会影响安全性, 这个攻击可以用于攻击交易所 无法正常完成交易.

解决延展性攻击: 对交易签名归一化, 规定使用数值小的那个签名. 

​							 把签名数据移到交易之外,不含签名的交易计算出来的哈希称为wtxid, 为此引入了一种新的隔离见证地址.



### HD钱包

如果一个用户控制的UTXO不是同一组地址, 则很难通过地址确定一个用户的持币总额.

管理一组地址, 意味着管理一组私钥, 很多的话管理起来就很麻烦.



**HD 分层确定性**, 有了根私钥可以通过索引计算出每一层的子私钥

<img src="https://gitee.com/lynbz1018/image/raw/master/img/20230208100832.png" alt="image-20230208100830154" style="zoom:80%;" />

私钥是一个扩展的512位私钥 **|** 通过SHA512算法和ECC计算出子扩展私钥 **|** 通过扩展私钥可以计算出用于签名的私钥和公钥

1. 根私钥可以计算出任意索引的子扩展私钥 `用户只保存一个根扩展私钥,即可管理所有私钥`
2. 扩展公钥在没有扩展私钥的前提下可以计算出任意下一层的扩展公钥 `可以把xpub交给第三方用于监控余额`
3. 扩展私钥能计算出扩展公钥

![image-20230208101442786](https://gitee.com/lynbz1018/image/raw/master/img/20230208101443.png)

扩展的层数没有限制, 每一层用于索引的有`4B`, 所以每一层的个数有`0~2^32`

<img src="https://gitee.com/lynbz1018/image/raw/master/img/20230208101608.png" alt="image-20230208101607271" style="zoom:80%;" />



**安全性**

如果某个`xprv`泄露了, 可以反向推导出上层的`xprv`, 继而推导出整个扩展私钥体系.

**硬化衍生计算方式**: 切断了母扩展私钥和子扩展私钥的反向推到.

索引`0~2^31` 为普通衍生索引

索引`2^31~2^32`为硬化衍生索引, 用`1' 2' 3' 表示 2^31+1 2^31+2 2^31+3`

硬化衍生索引 <u>1.不能由子扩展私钥反推出上层扩展私钥 2.扩展公钥也不能推导出子扩展公钥</u>

观察钱包能使用的索引是 `0~2^31`



#### 钱包层级

确定了根扩展私钥后, 整棵树的节点都可以扩展出来

```javascript
const bitcoin = require('bitcoinjs-lib');
let
    xprv = 'xprv9s21ZrQH143K4EKMS3q1vbJo564QAbs98BfXQME6nk8UCrnXnv8vWg9qmtup3kTug96p5E3AvarBhPMScQDqMhEEm41rpYEdXBL8qzVZtwz',
    root = bitcoin.HDNode.fromBase58(xprv);

// m/0:
var m_0 = root.derive(0);
console.log("xprv m/0: " + m_0.toBase58());  // 扩展私钥
console.log("xpub m/0: " + m_0.neutered().toBase58());  // 扩展公钥
console.log(" prv m/0: " + m_0.keyPair.toWIF());  // 私钥
console.log(" pub m/0: " + m_0.keyPair.getAddress());  // 公钥

// m/1:
var m_1 = root.derive(0);
console.log("xprv m/1: " + m_1.toBase58());
console.log("xpub m/1: " + m_1.neutered().toBase58());
console.log(" prv m/1: " + m_1.keyPair.toWIF());
console.log(" pub m/1: " + m_1.keyPair.getAddress());
```



可以在没有扩展私钥的情况下, 计算出子扩展私钥

```javascript
const bitcoin = require('bitcoinjs-lib');
let
    xprv = 'xprv9s21ZrQH143K4EKMS3q1vbJo564QAbs98BfXQME6nk8UCrnXnv8vWg9qmtup3kTug96p5E3AvarBhPMScQDqMhEEm41rpYEdXBL8qzVZtwz',
    root = bitcoin.HDNode.fromBase58(xprv);

// m/0:
let
    m_0 = root.derive(0),
    xprv_m_0 = m_0.toBase58(),
    xpub_m_0 = m_0.neutered().toBase58();

// 方法一：从m/0的扩展私钥推算m/0/99的公钥地址:
let pub_99a = bitcoin.HDNode.fromBase58(xprv_m_0).derive(99).getAddress();

// 方法二：从m/0的扩展公钥推算m/0/99的公钥地址:
let pub_99b = bitcoin.HDNode.fromBase58(xpub_m_0).derive(99).getAddress();

// 比较公钥地址是否相同:
console.log(pub_99a);  // 1GvmxzNG5i8EqXQuD75XaGjqf2oCEmJ87M
console.log(pub_99b);  // 1GvmxzNG5i8EqXQuD75XaGjqf2oCEmJ87M
```



不能从扩展公钥计算出硬化的子公钥

```javascript
const bitcoin = require('bitcoinjs-lib');
let
    xprv = 'xprv9s21ZrQH143K4EKMS3q1vbJo564QAbs98BfXQME6nk8UCrnXnv8vWg9qmtup3kTug96p5E3AvarBhPMScQDqMhEEm41rpYEdXBL8qzVZtwz',
    root = bitcoin.HDNode.fromBase58(xprv);

// m/0:
let
    m_0 = root.derive(0),
    xprv_m_0 = m_0.toBase58(),
    xpub_m_0 = m_0.neutered().toBase58();

// 从m/0的扩展私钥推算m/0/99'的公钥地址:
let pub_99a = bitcoin.HDNode.fromBase58(xprv_m_0).deriveHardened(99).getAddress();
console.log(pub_99a);

// 不能从m/0的扩展公钥推算m/0/99'的公钥地址:
bitcoin.HDNode.fromBase58(xpub_m_0).deriveHardened(99).getAddress();

```





##### **规范**

![image-20230208103238100](https://gitee.com/lynbz1018/image/raw/master/img/20230208103239.png)



#### 助记词

创建一个HD钱包需要一个512b的随机数种子

为了解决种子易用性问题, BIP-39提出了通过助记词推算种子

1. 挑选2048个单词构造一个单词数组
2. 生成一个128~256位的随机数, 随机数总位数是32的倍数
3. 随机数尾部加上HASH256的前若干位, 总数位数凑成11的倍数
4. 每11b一组, 得到(0, 2047)的24个整数, 对应单词数组索引获得一个助记词列表

```javascript
const bip39 = require('bip39');
let words = bip39.generateMnemonic(256);

console.log(words);
```



HD钱包要通过**助记词**和**口令**才能生成种子, 缺一不可.

```javascript
const bip39 = require('bip3');

let words = bip39.generateMnemonic(256);
console.log(words);

let password = 'bitcoin';

let seedAsHex = bip39.mnemonicToSeedHex(words, password);
console.log(seedAsHex);

```



```javascript
const
    bitcoin = require('bitcoinjs-lib'),
    bip39 = require('bip39');

let
    words = 'bleak version runway tell hour unfold donkey defy digital abuse glide please omit much cement sea sweet tenant demise taste emerge inject cause link',
    password = 'bitcoin';

// 计算seed:
let seedHex = bip39.mnemonicToSeedHex(words, password);
console.log('seed: ' + seedHex); // b59a8078...c9ebfaaa

// 生成root:
let root = bitcoin.HDNode.fromSeedHex(seedHex);
console.log('xprv: ' + root.toBase58()); // xprv9s21ZrQH...uLgyr9kF
console.log('xpub: ' + root.neutered().toBase58()); // xpub661MyMwA...oy32fcRG

// 生成派生key:
let child0 = root.derivePath("m/44'/0'/0'/0/0");
console.log("prv m/44'/0'/0'/0/0: " + child0.keyPair.toWIF()); // KzuPk3PXKdnd6QwLqUCK38PrXoqJfJmACzxTaa6TFKzPJR7H7AFg
console.log("pub m/44'/0'/0'/0/0: " + child0.getAddress()); // 1PwKkrF366RdTuYsS8KWEbGxfP4bikegcS
```



只要确定了助记词和口令, 生成的HD种子就确定了

助记词和口令丢失一个, 就会导致HD钱包丢失





#### 地址监控

HD钱包管理一组地址, 要监控链上的每个TX的输入和输出.

`m/44'/0'/0'/0/x` x可以有2^32个取值 数据很大.

**1.**查询数据库效率很低, **2.**通过哈希存到内存中速度快但是数量多了很占用内存

* HD钱包只会预生成前1000个地址（即索引号为0～999）并保存在本地数据库中，如果不够了，再继续扩展1000个，这样，HD钱包管理的地址数量不会太大。

* 每个元素通过若干个哈希函数映射成一个位数组的若干个点，将其置1。检索的时候，先计算给定元素对应位是否全1，如果是全1，则给定元素很可能存在，否则，元素必定不存在。



Bloom Filter判断时,如果不存在就肯定不存在, 存在的话实际上是以一定概率存在.

HD钱包通过Bloom Filter可以高效监控链上的所有地址，并根据是否是本地管理的地址决定如何计算钱包余额。



## 以太坊

以太坊是一个支持**智能合约**的区块链平台.

以太坊的账户模型是余额模型, 交易引发账户余额的变动, 和传统的金融账户一致.

以太坊实现了一个图灵完备的脚本语言, 运行在EVM(以太坊虚拟机)中, 任何人都可以编写合法的脚本执行任意逻辑.



### 账户

以太坊账户负责存储用户的以太坊余额.

* 外部账户: 普通用户用私钥控制的账户.
* 合约账户: 拥有合约代码的账户, 不属于任何人, 也没有私钥与之对应.



**外部合约**

一个以太坊账户就是一个公钥哈希后得到的地址, 公钥是通过私钥计算来的, 与比特币相同公钥的计算采用的是<u>椭圆曲线算法</u>, 但是以太坊使用的是**非压缩公钥**.

地址是对非压缩公钥(两个32B的哈希值) 进行keccak256哈希, 取后20B加上0x得到地址.

<img src="https://gitee.com/lynbz1018/image/raw/master/img/20230209142531.png" alt="image-20230209142529922" style="zoom:67%;" />

```javascript
const
    randomBytes = require('randombytes'),
    ethUtil = require('ethereumjs-util');
// 生成256bit的随机数作为私钥:
let priKey = randomBytes(32).toString('hex');
// 计算公钥(非压缩格式):
let pubKey = ethUtil.privateToPublic(new Buffer(priKey, 'hex')).toString('hex');
// 计算地址:
let addr = ethUtil.pubToAddress(new Buffer(pubKey, 'hex')).toString('hex');

console.log('Private key: 0x' + priKey);
console.log('Public key: 0x' + pubKey);
console.log('Address: 0x' + addr);
```

`keccak和标准的SHA3算法不同, keccak原本是SHA3的候选算法, 在标准化时对keccak进行了改进, 所以标准的SHA3和keccak不同, 以太坊在开发时使用的是未成为SHA3标准的keccak算法`

在讨论以太坊使用的哈希算法时使用的都是keccak256而不是标准的SHA3-256



**带校验的地址**

地址使用的是公钥hash后的后20B, 用十六进制表示的, 没有任何校验. 地址中任何一个数字出错仍是一个有效地址.

<u>通过大小写字母实现地址的校验,</u>  对地址做一个keccak256哈希, 按位对齐后, 把哈希值同为字母的变为大写

![image-20230209145518088](https://gitee.com/lynbz1018/image/raw/master/img/20230209145519.png)

好处: 带校验和不带校验的地址对软件钱包格式是一样的

缺点: 很小的概率无法校验全部是小写的地址



**HD钱包**

以太币和以太坊的非对称加密算法完全相同, 只是公钥和地址的表示格式不同,  多以比特币的**HD钱包体系**也完全适用于以太坊

通过一套助记词既可以管理比特币钱包,  也可以管理以太坊钱包

`60' 表示以太坊币种`



```javascript
// 助记词和口令:
let
    words = 'bleak version runway tell hour unfold donkey defy digital abuse glide please omit much cement sea sweet tenant demise taste emerge inject cause link',
    password = 'bitcoin';

// 计算seed:
let seedHex = bip39.mnemonicToSeedHex(words, password);
console.log('seed: ' + seedHex); // b59a8078...c9ebfaaa

// 生成root:
let root = bitcoin.HDNode.fromSeedHex(seedHex);
console.log('xprv: ' + root.toBase58()); // xprv9s21ZrQH...uLgyr9kF
console.log('xpub: ' + root.neutered().toBase58()); // xpub661MyMwA...oy32fcRG

// 生成派生key:
let child0 = root.derivePath("m/44'/60'/0'/0/0");
let prvKey = child0.keyPair.d.toString(16);
let pubKey = ethUtil.privateToPublic(new Buffer(prvKey, 'hex')).toString('hex');
let address = '0x' + ethUtil.pubToAddress(new Buffer(pubKey, 'hex')).toString('hex');
let checksumAddr = ethUtil.toChecksumAddress(address);

console.log("       prv m/44'/60'/0'/0/0: 0x" + prvKey); // 0x6c03e50ae20af44b9608109fc978bdc8f081e7b0aa3b9d0295297eb20d72c1c2
console.log("       pub m/44'/60'/0'/0/0: 0x" + pubKey); // 0xff10c2376a9ff0974b28d97bc70daa42cf85826ba83e985c91269e8c975f75f7d56b9f5071911fb106e48b2dbb2b30e0558faa2fc687a813113632c87c3b051c
console.log("      addr m/44'/60'/0'/0/0: " + address); // 0x9759be9e1f8994432820739d7217d889918f2f07
console.log("check-addr m/44'/60'/0'/0/0: " + checksumAddr); // 0x9759bE9e1f8994432820739D7217D889918f2f07
```





### 区块结构

以太坊存储用户数据的数据结构是MPT(Merkle Patricia Tree),  当MPT中的每一个叶子确定后,  计算出Root Hash就是完全确定的.

如果发生转账, 将会计算出一个新的Root Hash

从全局看,  以太坊就像一个状态机,  每个区块记录一个stateRoot来表示一个新的状态,  因此stateRoot被称作当前的世界状态.

`每个区块记录的数据只包括修改的部分, 实际上记录的只有修改的账户以及导致上层发生变化的Hash`

`每个节点的数据被存放到LevelDB, 节点仅在内存中存放当前活跃的账户信息,  需要操作的账户不在内存中就从LeveDB中读取,  如果内存不够也会将内存中长期没活动的节点移除,  将来可以通过节点的路径再次从LevelDB中恢复`

![image-20230209151910851](https://gitee.com/lynbz1018/image/raw/master/img/20230209151911.png)

**账户数据**

* nonce  递增整数,  每发生一次交易就递增1,  记录的就是交易次数
* balance  记录账户余额,  以wei为单位,  1Ether 等于 10^18wei
* storageRoot  如果是合约账户 存储合约相关的状态数据
* codeHash  存储合约代码的Hash

如果是外部账户storageRoot 和 codeHash都是空的



**区块数据**

一个以太坊区块由区块头部和交易信息构成,  区块头部记录有parentHash(上一个区块的Hash)  stateRoot(世界状态),  还有:

- sha3Uncles：记录引用的叔块；
- transactionRoot：记录当前区块所有交易的Root Hash；
- receiptsRoot：记录当前区块所有交易回执的Root Hash；
- logsBloom：一个Bloom Filter，用于快速查找Log；
- difficulty：挖矿难度值；
- number：区块高度，严格递增的整数；
- timestamp：区块的时间戳（以秒为单位）；

transactionRoot 和 receiptsRoot 仅表示当前区块的两棵树,  和前边的区块状态无关



**叔块**

#4的竞争失败, 导致一个挖矿成功另一个失败, 以太坊鼓励后序的#5区块引用另一个废弃的#4区块,  这种引用的废弃块被称为叔块

叔块的目的是给予竞争失败的矿工部分奖励,  避免出现较长的分叉.

![image-20230209153954693](https://gitee.com/lynbz1018/image/raw/master/img/20230209153955.png)



### 交易

以太坊交易中也需要手续费, 手续费被称为Gas

以太坊支持 1. 从一个账户支付Ether到另一个账户

​					 2.执行合约代码, 合约代码是图灵完备的编程语言, 通过EVM执行

为了保证合约代码的<u>可靠执行</u>, 以太坊给每一个虚拟机指令到标记了一个GadUsed:  加减计算的费用是3，计算SHA3的费用是30，输出日志的费用是375，写入存储的费用高达20000。

`消耗cpu比消耗存储便宜, 简单计算比复杂计算便宜, 读取比写入便宜`

用户需要提供一个Gas Price, 以Gwei为单位 1Gwei = 10^9wei, 通过竞价得到一个矿工愿意的接受的gasPrice  `如果交易少了,Gas Price下降, 如果交易多了网络拥堵, 则Gas Price上升`

 交易费用是gasUsed \* gasPrice

* 以太坊规定,  一笔交易先给出gasPrice和gasLimit, 如果执行完有剩余就退回, 执行过程中耗尽则交易执行失败, 但已执行的Gas不会退回

* 给出gasPrice为50 Gwei, 预估gasUsed为120000, 设定gasLimit为150000

  ```markdown
  预支付为
  150000 * 50Gwei = 750000Gwei = 0.0075Ether
  如果账户余额不足0.0075, 交易根本无法发送
  如果账户余额大于等于0.0075, 则矿工可以将该交易打包, 如果实际消耗gasUsed为120000, 则交易费用为0.006,账户会扣除这部分交易费用
  ```

* 很少有交易可以准确预估gasUsed, 只有标准转账交易是21000, 所以标准转账交易的gasLimit可以设置成21000



### 交易回执

以太坊区块为每一笔交易都会产生一笔回执（Recipt），表示交易的最终状态。一个回执信息主要包括：

- status：执行结果，1表示成功，0表示失败；
- gasUsed：已消耗的Gas数量；
- txHash：交易Hash；
- logs：交易产生的日志；
- ……

### 转账交易

转账交易是指两个外部账号转移Ether，我们以测试网的交易[0xf04d...b7ba](https://ropsten.etherscan.io/tx/0xf04dfc4f3fe7d7623abbc3ae1e4a6e4f20d14b9db134d573f224dc2994feb7ba)为例，可以看到：

- Transaction Hash: 0xf04d...b7ba，这是交易Hash，即交易的唯一标识；
- Status: Success，表示交易成功；
- From: 0x0c46...2978，交易的发送方；
- To: 0x77e4...e34c，交易的接收方；
- Value: 0.02759796846726396 Ether，交易发送的Ether；
- Gas Price: 1.500000788 Gwei，Gas的价格；
- Gas Limit: 21,000，转账交易恰好消耗21000Gas，因此总是21000；
- Gas Used by Transaction: 21,000 (100%)，消耗的Gas占比，这里恰好全部消耗完；
- Nonce：1，发送方的nonce，1表示第2笔交易；
- Input Data: 0x，因为是转账交易，没有输入数据，因此为空。

### 合约交易

合约交易就是指一个外部账号调用某个合约的某个public函数。我们以测试网的交易[0x2235...132e](https://ropsten.etherscan.io/tx/0x223572134e999599c24d255e1beee78c8c33dcc52262a9ef5524f8f2a552132e)为例，可以看到：

- From: 0x0c46...2978，交易的发起方，该地址一定是外部账户；
- To: 0x5b2a...5a46，交易的接收方，这里地址是一个合约地址；
- Value: 0 Ether，这里发送的Ether是0，即没有向合约发送Ether；
- Gas Limit: 105,406，这是交易发起前设定的最大Gas；
- Gas Used by Transaction: 70,271 (66.67%)，这是交易实际消耗的Gas；
- Input Data: 0xb3f98adc...，这是交易的输入数据，其中包含了调用哪个函数，以及传递的参数。



### 智能合约

以太坊和比特币相比最大的创新就是以太坊支持**智能合约**

智能合约:  **运行在区块链上的程序**.  

* 智能合约要保证在区块链网络中的每一个节点运行的结果完全相同  这样才可以使 <u>任意一个节点</u> 都可以验证  <u>挖矿产出节点</u> 生成的区块里 智能合约执行的结果对不对.

以太坊提供了一个**EVM**(以太坊虚拟机)用于执行智能合约的字节码.

为了消除智能合约的不确定性,  **智能合约有很多限制,**  如不支持浮点计算(浮点表示方法不同, 不同的CPU运算符的浮点结果也不相同)

* 以太坊提供了**Solidity**高级语言编写智能合约,  编译为智能合约字节码后,  可以在EVM中执行.

* 智能合约的字节码在部署在区块链时,  会根据部署着的地址和该地址的nonce分配一个**合约地址**
  * 合约地址**没有私钥**,  没有人可以直接调用改地址的合约数据
  * 调用合约唯一的方法是:  **调用合约的公共函数**
* 合约不能主动执行,  智能被外部账户发起调用
  * 如果需要一个人合约定期执行,  需要线下服务器定期发起合约调用
  * 合约在执行时可以调用其他合约的公共函数
* 合约作为地址,  既可以接受Ether,  也可以发送Ether.
  * 合约也可以存储数据,  数据存储在地址关联的存储上,  这就使得**合约具有了状态**

`合约在运行过程可以调用其他已经部署的合约, 要知道合约的地址和函数签名`

`一个合约可以调用另一个借贷合约的借款方法, 在调用交易方法, 最后调用还款方法, 快速实现一个带宽交易`

`多个合约的嵌套调用, 可能会使代码因漏洞被黑客攻击的风险增大`





#### 编写合约

以太坊的智能合约就是运行在EVM虚拟机上的字节码.

用高级语言**Solidity**(类JavaScript语法的高级语言)编写后通过编译器编译为字节码.

```javascript
// SPDX-License-Identifier: GPL-3.0   ** 版权声明

pragma solidity =0.8.7;  //  ** 声明编译器版本
// pragma solidity >=0.8.0 <0.9.0;  //  ** 制定版本范围 0.8.x

contract Vote {  //  ** 由关键字 'contract' 声明一个合约
// 一个solidity文件可以包含多个合约 最好一个文件一个合约
// 文件名要和合约名保持一致

    // 合约可以定义事件, 触发事件必须在合约 写函数 中通过 emit 关键字实现
    // 事件可以用于通知外部感兴趣的第三方, 他么可以在区块链上监听产生的事件, 从而确定合约某些状态发生了改变
    event Voted(address indexed voter, uint8 proposal);

    mapping(address => bool) public voted;  // 记录已投票的地址

    uint256 public endTime;  // 记录终止时间
	
    // 支持整型(uint256 uint128 uint8) byte32 映射类型(相当于map) 布尔型(false true) 特殊的address类型(表示一个以太坊地址)
    // 为了保证每一个节点运行智能合约的结果完全相同 不支持浮点类型
    // 所有的类型默认初始化为 0 或 false 或 空
    uint256 public proposalA;  // 记录每个人得到的票数
    uint256 public proposalB;
    uint256 public proposalC;
	
    // 如果某个成员变量要指定初始值, 需要在构造函数中复制
    constructor(uint256 _endTime) {
        endTime = _endTime;  // 设定成员变量为指定参数值
    }
	
    // 没有view修饰的函数是写入函数, 会改变成员变量, 即改变了合约状态
    function vote(uint8 _proposal) public {
        require(block.timestamp < endTime, "Vote expired.");
        require(_proposal >= 1 && _proposal <= 3, "Invalid proposal.");
        require(!voted[msg.sender], "Cannot vote again.");
        voted[msg.sender] = true;
        if (_proposal == 1) {
            proposalA ++;
        }
        else if (_proposal == 2) {
            proposalB ++;
        }
        else if (_proposal == 3) {
            proposalC ++;
        }
        emit Voted(msg.sender, _proposal);  // 调用vote()写方法时, 会触发Voted事件
    }
	
    // 用view修饰的函数是只读函数, 不会修改成员变量, 即不会修改合约的状态
    function votes() public view returns (uint256) {
        return proposalA + proposalB + proposalC;
    }
}
```

**合约要素**

* 版权声明
* 声明编译器版本
* contract关键字声明合约
* 包含若干成员变量
* 在构造函数中对成员变量指定初始化
* 编写只读方法
* 编写写入方法
* 可以声明Event并在写入方法中触发

函数被`public`修饰, 该函数可以被外部调用, 被`private`修饰, 该函数只能被`public`函数在内部调用



**合约执行流程**

合约编写完并成功编译后,就可以部署到以太坊上,合约部署后自动获得一个地址, 通过地址即可访问合约.

合约相当于一个类, 部署一次相当于一个实例化, 如果部署两次, 将得到两个不同的地址, 两个部署后的合约的成员变量也是相互独立的.

* 合约部署时构造函数就会立刻执行一次, 且仅执行一次. 
  * 合约部署后就无法调用构造函数

* 任何外部账户都可以发起对合约的调用
  * 如果调用**只读方法**, 因为不改变合约状态, 任何时刻可以调用, 不需要签名,也不消耗Gas
  * 如果调用**写入方法**, 需要签名提交一个交易, 且消耗Gas
* 一个交易中只能调用一个合约的一个写入方法
  * 以太坊交易中写入是严格串行的

**验证**

因为任何外部账户都可以调用合约的函数, 多以任何验证工作都是在函数内部自行完成的

```javascript
// require() 可以断言一个判断 如果断言失败 将抛出错误并中断执行
//参数检查 参数必须为1 2 3
require(_proposal >= 1 && _proposal <= 3, "Invalid proposal.");

// 条件检查 时间必须小于设定的结束时间
require(block.timestamp < endTime, "Vote expired.");

// 调用方检查 不能重复调用
require(!voted[msg.sender], "Cannot vote again.");
```



如果中途失败, 则合约的状态保持不变, 失败前改变的成员变量也不会发生修改

```javascript
function increment() {
    // 假设a,b均为成员变量:
    a++;
    emit AChanged(a);
    // 如果下面的验证失败，a不会被更新，也没有AChanged事件发生:
    require(b < 10, 'b >= 10');
    b++;
}
```

合约执行失败后, 合约的状态不发生变化, **仅仅是调用方白白消耗了Gas**



#### 部署合约

**部署合约**也是一个交易, 需要一个**外部账户**, 消费一定的Gas

MetaMask钱包是一个基于浏览器插件的钱包, 使用时通过Dapp网站的JavaScript可以发起交易, 用户通过MetaMask确认后就可以将交易发送至链上.

MetaMask插件: [安装地址](https://chrome.google.com/webstore/detail/metamask/nkbihfbeogaeaoehlefnkodbefgpgknn/related)

MetaMask可以切换不同的链, 以太坊主链 Ropsten测试网 Rinkeby测试网等

在开发阶段可以使用Ropsten测试网

* 以太坊官方提供了一个在线IDE, 可以用于编写 编译 部署以太坊合约 [Remix](http://remix.ethereum.org/)



1. 在contracts文件夹中编写一个合约

![image-20230212112945154](https://gitee.com/lynbz1018/image/raw/master/img/20230212113210.png)



2. 进行编译

![image-20230212113026116](https://gitee.com/lynbz1018/image/raw/master/img/20230212113027.png)



3. 进行部署

![image-20230212113219252](https://gitee.com/lynbz1018/image/raw/master/img/20230212113220.png)





#### 调用合约

部署合约的合约地址`0x45bcada03c3b74d33e4452b513e45ca8a7f7bb89`

<img src="https://gitee.com/lynbz1018/image/raw/master/img/20230212120002.png" alt="image-20230212120001495" style="zoom:80%;" />



在[Etherscan](https://goerli.etherscan.io/) 输入合约地址搜索查看

通过'Verify and Publish' 将源码传到Etherscan并验证

![image-20230212120134785](https://gitee.com/lynbz1018/image/raw/master/img/20230212120135.png)



只读函数不需要耗费Gas, public字段会自动对应一个只读的函数

![image-20230212120330273](https://gitee.com/lynbz1018/image/raw/master/img/20230212120331.png)



写入函数 会改变合约状态 会消耗Gas

![image-20230212120410288](https://gitee.com/lynbz1018/image/raw/master/img/20230212120411.png)



调用了写入函数, 同时也触发了里面的时间事件

<img src="https://gitee.com/lynbz1018/image/raw/master/img/20230212120453.png" alt="image-20230212120452013" style="zoom:80%;" />



#### 编写Dapp

可以在Etherscan中调用读取函数和写入函数, 这对于普通用户过于繁琐 和 不方便

可以编写一个Dapp, 在网页通过按钮可以调用合约.

<img src="https://gitee.com/lynbz1018/image/raw/master/img/20230212121118.png" alt="image-20230212121117786" style="zoom:80%;" />

1. 页面的JavaScript无法直接访问以太坊网络的P2P节点, 只能通过钱包间接访问
2. 钱包之所以能访问以太坊网络节点, 是因为他内部部署了某些公共节点的域名
3. 所以一个浏览器用户没有安装MetaMask钱包, 则无法通过钱包读取合约和写入



Dapp部署一个服务器后, 由服务器端连接P2P网络节点并读取合约, 然后以JASON API的形式给前端提供相关数据.

<img src="https://gitee.com/lynbz1018/image/raw/master/img/20230212122642.png" alt="image-20230212122641486" style="zoom:80%;" />

1. 后端服务只读取合约, 不存取任何私钥, 因此无法写入合约, 保证了安全性
2. 后端服务器读取合约, 可以选择公共的服务节点
3. 后端服务器应该通过合约产生的日志(写入合约运行时出发的event)监听合约的变化. 监听日志需要通过P2P节点创建Filter并获取Filter返回的日志
4. 后端服务器将从日志获取的数据做好聚合 缓存以便前端页面能快速展示相关的数据.



一个好的Dapp既要考虑关键业务逻辑 写入合约, 又要考虑日志输出有足够的信息让后端服务器聚合数据.

需要前端 后端 合约三方开发紧密配合.





#### 常用合约

