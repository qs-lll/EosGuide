## cleos创建账户指南
#### 创建钱包
###### 钱包是授权对区块链执行操作所必需的私钥库。这些密钥存储在使用为您生成的密码加密的磁盘上。该密码应存储在安全的密码管理器中。
```
$ cleos wallet create -n xxwallet

Creating wallet: xxwallet
Save password to use in the future to unlock this wallet.
Without password imported keys will not be retrievable.
"PW5KhQiLdSAt5yNLqdMsAQnEXWbpu5WxitN1fVykWWmXkrJdLx8RL"
```
###### 钱包在不使用或者离开的时候,锁定钱包而不关闭
```
$ cleos wallet lock -n xxwallet
Locked: xxwallet
```
###### 解锁钱包
```
$ cleos wallet unlock -n xxwallet
password: 
```
###### 使用明文密码解锁钱包
```
$ cleos wallet unlock -n xxwallet --password PW5KhQiLdSAt5yNLqdMsAQnEXWbpu5WxitN1fVykWWmXkrJdLx8RL
Unlocked: xxwallet
```
#### 创建账户
1. 创建密钥  
	`
	cleos create key
	`
	
	```
	Private key: 5K4Ei4tEqePm2xcpAoqCjKtmdh84VpVwhHMNvC3tbptQ2UugeTH  
	Public key: EOS7Zj2kQ26J8kWaXjfK9jvSf4rju3VR5oW5ekBZFTvGydUuwHJ5u
	```
	
2. 导入钱包  
	```
	cleos wallet import 5K4Ei4tEqePm2xcpAoqCjKtmdh84VpVwhHMNvC3tbptQ2UugeTH -n xxwallet
	```
	
3. 通过主网创建账户(首先要有一个账户才能创建,没有的话需要找有账户的朋友创建一个)
	```
cleos -u http://mainnet.genereos.io system newaccount --stake-net '0.0010 EOS' --stake-cpu '0.0010 EOS' --buy-ram-kbytes 8 youraccountname newaccountname
	```

#### 官方解释
##### What is an EOS account?
> 
An account is a human-readable name that is stored on the blockchain.
An account is required to transfer or otherwise push a transaction to the blockchain.

>
帐户是存储在区块链中的人类可读名称。
需要账户才能将交易转移或以其他方式推送到区块链。

##### Can I change my account name?
>
Not until the EOS mainnet launches. After the mainnet launches, you will be able to create new account names. The actual ins and outs will be announced.
>
直到EOS主网启动。 主网络启动后，您将能够创建新的帐户名称。 实际情况将会公布。

##### Will my account name change?
>
It is unlikely to change at this point. Please come back later to check if your account name has changed.
>
这一点不太可能改变。 请稍后再回来检查您的帐户名称是否已更改。

##### How are account names assigned?
>
All EOS account names on launch are 12 characters long. The account names are based on when the Ethereum wallet was first seen also padding genesis at the end.
>
所有推出的EOS帐户名称长度为12个字符。 账户名是根据Ethereum钱包第一次出现的时间以及最后填充的起源。

##### What is block one's account name?
>
Well Block one gets to keep the awesome account name: b1
>
Block one 保持帐户名称：b1

##### I can't find my account name!
>
Have you completed your EOS registration process? If you have, please wait for us to update our snapshot.
>
您是否完成了EOS注册流程？ 如果有，请等待我们更新我们的快照。