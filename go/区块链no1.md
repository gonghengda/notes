### 课程大纲：

> 区块链主要开发工具 go、c++、node。js
> 认识区块链
  - 区块链不是一个新的技术，区块链是一种新型的应用模型，分布式存储，点对点的传输协议，**加密**、**共识算法本质**，去中心化的分布式数据库
  - 去中心化与中心化
  - 全节点钱包
  - 区块链的发展：
    - 比特币1.0
    - 以太坊2.0 （去中心化的应用平台）
    - EOS 3.0

> 认识以太坊
  - 去中心化的应用平台、允许任何人在该平台上运行基于区块链技术的DAPP（去中心化的分布式应用）
  - 区块链底层技术，开发人员只需要专注于上层应用的开发，极大的降低开发难度。
  - EVM：以太坊智能合约的运行环境
  - 智能合约   合同
    - 没有法律层面的一个完整的定义，在计算科学领域：一个协议，自我执行与自我校验的功能
    - 优势： 实时高效 去中心化权威，维护成本
    - [以太坊官网](https://etherscan.io)
> 实战搭建以太坊开发环境 （以太坊底层开发语言go语言）
  - 安装geth  
    - 以太坊钱包：geth控制台钱包 （可以转账。。。）也有图形化界面 
    - imtoken 手机钱包
  - 安装solc（remix）
  - truffle以及testrpc（能快速生成以太坊测试账号）

> solidity实战
  - 
> 实战ICO（发币）
  - 查看以太坊官方数
  ```shell
  获取轻钱包
  选取一个TOKEN 修改智能合约代码
  编译 部署
  ```

4.以太坊平台对底层区块链技术进行了封装，让区块链应用开发者可以直接基于以太坊平台进行开发，开发者只要专注于应用本身的开发，从而大大降低了难度。a.什么是以太坊？1.在计算机科学领域，智能合约是指一种计算机协议。这类协议一旦部署就能自我执行和自我验证，不再需要人为干预1.高效的实时更新2.准确执行3.较低的人为干预风险4.去中心化权威5.较低的运行成本2.智能合约的优点：1.The DAO攻击事件：合约存在漏洞导致大量以太币被盗，而且因为智能合约的去人为干预特性，使得漏洞无法线上修复。最终采用的办法是分叉。所以，智能合约需要保证合约代码的逻辑完整性和安全性，否则一旦受到攻击，后果会非常严重3.缺点：b.什么是智能合约？1.EVM（Ethereum Virtual Machine）以太坊虚拟机是以太坊中智能合约的运行环境。c.以太坊运行环境：EVM1.Solidity以太坊智能合约的官方推荐的编程语言，文件扩展名以.sol结尾。2.它是一个类javascript的、图灵完备的编程语言3.以太坊的编程语言还有Viper，Serpent，LLL及Bamboo，但推荐使用d.什么是solidity？初识以太坊与智能合约2.以太坊环境搭建与智能合约Solidity简介2018年7月3日11:12分区 以太坊与智能合约 的第1 页
3.以太坊的编程语言还有Viper，Serpent，LLL及Bamboo，但推荐使用solidity1.sudo add-apt-repository ppa:git-core/ppa2.sudo apt-get update3.sudo apt-get install git安装git1.1.git --version查看git版本号2.1.sudo apt-get install software-properties-common2.sudo add-apt-repository -y ppa:ethereum/ethereum3.sudo apt-get update4.sudo apt-get install ethereum3.安装geth1.geth --help4.获取geth指令1.sudo add-apt-repository ppa:ethereum/ethereum2.sudo apt-get update3.sudo apt-get install solcsolc安装(本课采用在线IDE Remix)5.1.下载源码地址：https://nodejs.org/en/download/2.解压&&进入node目录3../configure4.make && make install5.1.node -v2.npm -v 查看版本6.1.truffle和testrpc是配套的以太坊开发框架。通过truffle可以快速的编译和部署合约并进行测试，同时还有web前端交互界面2.testrpc可以理解为快速生成以太坊测试账号3.1.npm config set registry https://registry.npm.taobao.org2.npm install -g truffle3.npm install -g ethereumjs-testrpc由于被墙的原因，安装truffle比较慢，先设置淘宝源4.1.truffle --version查看版本号truffle和testrpc6.npm安装以太坊+Solidity开发环境搭建3.1.以太坊钱包也就是我们的以太坊客户端、其实我们可以把它理解为一个开发者工具，它提供账户管理、挖矿、转账、智能合约的部署和执行等等功能以太坊钱包介绍4.分区 以太坊与智能合约 的第2 页
具，它提供账户管理、挖矿、转账、智能合约的部署和执行等等功能2.钱包分两种一种是交互式命令的控制台就是我们上面所说的geth，另一种是图形化钱包以太坊有各种图形化钱包，包括电脑端和手机端的、目前最常用的是Mist solidity在线编译IDE:remix1.启动一个以太坊节点geth --datadir data --dev console 2>>logs.txt2.使用solidity编写智能合约3.编译智能合约4.将编译好的合约代码部署到以太坊上5.使用web3.js库所提供的js api调用合约5.智能合约的部署流程6.没有hello world的程序是不完整的程序--按照步骤5 实现hello world智能合约7.1.google安装轻钱包metamask2.查看以太坊数据:https://etherscan.io3.查看波厂合约1.修改合约代码并编译2.部署到指定的地址上创建token3.设置gas并提交验证4.交易测试
