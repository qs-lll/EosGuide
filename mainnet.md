#####查询余额(当前合约的余额)
```
cleos -u http://mainnet.genereos.io get currency balance nrenaissance g44dgnbqgige ARTCOIN
```
#####部署发币合约
```
cleos -u http://mainnet.genereos.io set contract nrenaissance build/contracts/eosio.token -p nrenaissance
```
#####执行发币_创建
```
cleos -u http://mainnet.genereos.io push action nrenaissance create '[ "nrenaissance", "20679750.0000 ARTCOIN"]' -p nrenaissance
```
#####派发
```
cleos -u http://mainnet.genereos.io push action nrenaissance issue '[ "g44dgnbqgige", "100.0000 SYS", "memo-test" ]' -p nrenaissance
```
#####转账
```
cleos -u http://mainnet.genereos.io push action nrenaissance transfer '[ "g44dgnbqgige", "buaabuaabuaa", "100.0000 ARTCOIN", "test transfer" ]' -p g44dgnbqgige
```
#####购买ram
```
cleos -u http://mainnet.genereos.io system buyram nrenaissance nrenaissance '0.5 EOS'
```
#####抵押cpu bandwidth
```
cleos -u http://mainnet.genereos.io system delegatebw nrenaissance nrenaissance '0.5 EOS' '0.5 EOS'
```
#####创建账户
```
cleos -u http://mainnet.genereos.io system newaccount --stake-net '0.0010 EOS' --stake-cpu '0.0010 EOS' --buy-ram-kbytes 8
```
#####获取ram价格
```
cleos -u http://mainnet.genereos.io get table eosio eosio rammarket
```

--

#####wast
```
$ eosiocpp -o hello.wast hello.cpp
```
#####abi
```
$ eosiocpp -g hello.abi hello.cpp
```
#####运行合同
```
$ cleos push action hello.code hi '["user"]' -p user
```
#####监视输出
```
如果您正在观察输出nodeos，
您可能没有看到任何nodeos指示发生任何事情的输出。
您可以nodeos使用该--contracts-console选项重新启动，以将打印的调试输出发送到控制台。

```