##### 获取汇率
命令行获取汇率:

```
cleos -u http://mainnet.genereos.io get table eosio eosio rammarket
```

python获取汇率:

```
##ram coin rate

import requests              
import json

rate = requests.post('http://mainnet.genereos.io/v1/chain/get_table_rows',data='{"json":"true","scope":"eosio","code":"eosio","table":"rammarket"}',headers={'Content-Type':'application/json'})
rateL = json.loads(rate.text)
content = rateL.__getitem__("rows")[0]
balance = content.__getitem__("base").__getitem__("balance").split(" ")[0]
quote = content.__getitem__("quote").__getitem__("balance").split(" ")[0]
print("1 EOS = "+ str(float(balance)/float(quote)/float(1000))+" KB")
print("1 KB = "+ str((float(quote)/float(balance)*1000))+" EOS")
```
#### 交易
##### 买入:
```
cleos -u http://mainnet.genereos.io system buyram XXXXX XXXXX '0.5 EOS'
```
##### 卖出:


```
cleos -u http://mainnet.genereos.io system sellram XXXXX '0.5 EOS'
```
