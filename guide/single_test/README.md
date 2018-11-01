##### 单节点运行eos节点并执行合约

创建账号
```
cleos create account eosio eosio.token EOS7euSibKMYbDWXDHgVDgFQB4TpyYeSu...... EOS7euSibKMYbDWXDHgVDgFQB4TpyYeSu......
```
部署合约
```
cleos set contract eosio.token /Users/qs/Documents/eos/contracts/eosio.token
```
创建代币
```
cleos push action eosio.token create '[ "eosio", "1000000000.0000 EOS"]' -p eosio.token
```
发币(eosio.token, account, eosio)
```
cleos push action eosio.token issue '[ "account", "100.0000 SYS", "memo-test" ]' -p eosio
```
合约账号授权 eosio.code
```
cleos set account permission game active '{"threshold": 1,"keys": [{"key": "EOS7vbv8nQpFMZmYiH3pGSHFUAoa4bL33zr2ZDGk.......","weight": 1}],"accounts": [{"permission":{"actor":"game","permission":"eosio.code"},"weight":1}]}' owner -p game
```
cpp
```
 eosiocpp -o /Contract/test/test.wast /Contract/test/test.cpp
 ```
 ```
 eosiocpp -g /Contract/test/test.abi /Contract/test/test.cpp
 ```
部署合约
```
cleos set contract game /Contract/test -p game
```

