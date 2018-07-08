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
  - EVM：（Ethereum Virtual Machine）以太坊虚拟机是以太坊中智能合约的运行环境
  - 以太坊运行环境：EVM1
  - Solidity以太坊智能合约的官方推荐的编程语言，文件扩展名以sol结尾。
  - 智能合约   合同
    - 没有法律层面的一个完整的定义，在计算科学领域：一个协议，自我执行与自我校验的功能
    - 优势： 实时高效 去中心化权威，维护成本，准确执行
    - [以太坊官网](https://etherscan.io)
  - 以太坊的编程语言还有Viper，Serpent，LLL及Bamboo，但推荐使用solidity
  - 查看以太坊数据:https://etherscan
> 实战搭建以太坊开发环境 （以太坊底层开发语言go语言）
  - 安装geth  
    - 以太坊钱包：geth控制台钱包 （可以转账。。。）也有图形化界面 
    - imtoken 手机钱包
    - google安装轻钱包metamask2
  - 安装solc（remix）
    - 钱包分两种一种是交互式命令的控制台就是我们上面所说的geth，另一种是图形化钱包以太坊有各种图形化钱包，包括电脑端和手机端的、目前最常用的是Mist       - solidity在线编译IDE:remix
  - truffle以及testrpc
    - 是配套的以太坊开发框架。
    - 能快速生成以太坊测试账号
    - 通过truffle可以快速的编译和部署合约并进行测试，同时还有web前端交互界面
    ```shell
    npm install -g truffle
    ```

> solidity实战
  - Solidity以太坊智能合约的官方推荐的编程语言，文件扩展名以
sol结尾
> 实战ICO（发币）
  - 查看以太坊官方数
  ```shell
  获取轻钱包
  选取一个TOKEN 修改智能合约代码
  编译 部署
  ```

安装geth1
geth --help 获取geth指令
sudo add-apt-repository ppa:ethereum/ethereum2
sudo apt-get update3
sudo apt-get install solcsolc安装(本课采用在线IDE Remix)5

npm config set registry https://registry
npm install -g truffle


truffle --version查看版本号truffle和testrpc6
启动一个以太坊节点geth --datadir data --dev console 2>>logs

