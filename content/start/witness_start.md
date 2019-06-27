---
title: "见证人节点"
date: 2019-06-25T17:23:52+08:00
draft: false
menu:
    docs:
      parent: "start"
---

如果你想成为 Nerthus 的见证人，本文给你提供指引。
从开始申请，到最终参与见证工作，依次需要做如下工作：

1. 部署节点
2. 申请加入
3. 开启见证服务
4. 服务器维护

## 部署节点

在开始参与见证前，需要提前准备部署一个见证节点，并且完整同步 Nerthus 区块数据。为开启见证服务做准备。

### 服务器配置要求

根据 Nerthus 开发团队的测试结果。为了保证及时高效地处理交易，推荐的见证节点服务配置信息如下。

+ CPU: 8 核，主频2.5Ghz 以上。
+ 内存：36GB
+ 网络带宽： 10MB
+ 磁盘：两个 SSD 硬盘，40GB 系统盘和200GB 数据盘。
+ 操作系统：Linux ，推荐 CentOS 7

请根据推荐配置购买服务器，如果你的服务器和其他见证人的配置相差甚远。
直接影响是，参与见证工作的效率不高，影响到见证收益。

### 服务器安全配置

下面是一些必然要处理的服务器**基础**安全设置（不表示服务器已完全安全），请按照步骤依次设置。

```sh
wget https://github.com/nerthus-foundation-ltd/nerthus/blob/master/scripts/witness/server_sec.sh
# 执行设置
./server_sec.sh
```

作为见证节点，**需要防护服务器**，减低被黑客攻击风险。
推荐阅读阿里云官方的安全技术文档-[Linux操作系统加固](https://help.aliyun.com/knowledge_detail/49809.html)。

### 安装 Nerthus 环境

使用上面创建的账户 nerthus 登录服务器。
```
sh -u nerthus
cd $HOME/.nerthus/env
wget https://github.com/nerthus-foundation-ltd/nerthus/blob/master/scripts/witness/witness_cli.sh
# 初始化环境
./witness_cli.sh init
# 安装 Nerthus
./witness_cli.sh install
```


### 运行节点
```sh
systemctl start cnts
```
此时，你可以登录到 Nerthus 的 JS 执行环境中，管理 Nerthus。
```sh
./witness_cli.sh attach
```

## 申请加入见证人
建议通过钱包申请成为见证人，操作手册见：[申请成为见证人](https://github.com/nerthus-foundation-ltd/wallet/wiki/Manual#申请成为用户见证人系统见证人)

成为见证人，需要由理事会发起招募信息。
当理事会成员发出招募新见证人提案时，在钱包的议案菜单中可以看到此招募信息。
此时任何人均有资格申请成为见证人，但需要缴纳保证金至少60万(NTS)。

招募见证人议案的参选时间为 960 个系统链单元时间（约 1 天）。在此期间见证人可追加保证金。
在招募结束后(1天)，系统将选出参选通过的用户成为见证人。
如果实际参与招募的见证人人数高于招募人数上限（有效用户见证人上限1万名）时，将根据保证金从高到底排名，依次选取见证人，直到足额。
没有选上的见证人将退还保证金。

一旦成功成为见证人，则必须在短时间内在已部署的节点上开启见证服务。
如果未能及时工作，将有三点惩罚：

1. 无法获得保证金利息收入。
2. 无法获得见证奖励。
3. 2 天内尚未参与见证的，将被拉黑，且扣罚15%的保证金。

## 开启见证
当数据同步完成，且自己已经是见证人时，可以开启见证服务。

如果见证人账户的 keystore 文件在服务器还不存在则需要先导入账户到服务器：
```
cd $HOME/.nerthus/env
./cnts --testnet account import  <keyfile>
```
在节点运行后，可执行命令启动见证服务。
```
witness_cli.sh --start_witness
```




