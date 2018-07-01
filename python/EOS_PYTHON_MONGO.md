# 分析EOS主网数据

本文提出了一种分析EOS主网数据的方法  

cleos命令行查询block返回的数据是json格式  
```
$ cleos get block 1
{
  "timestamp": "2018-06-08T08:08:08.500",
  "producer": "",
  "confirmed": 1,
  "previous": "0000000000000000000000000000000000000000000000000000000000000000",
  "transaction_mroot": "0000000000000000000000000000000000000000000000000000000000000000",
  "action_mroot": "aca376f206b8fc25a6ed44dbdc66547c36c6c33e3a119ffbeaef943642f0e906",
  "schedule_version": 0,
  "new_producers": null,
  "header_extensions": [],
  "producer_signature": "SIG_K1_111111111111111111111111111111111111111111111111111111111111111116uk5ne",
  "transactions": [],
  "block_extensions": [],
  "id": "00000001405147477ab2f5f51cda427b638191c66d2c59aa392d5c2c98076cb0",
  "block_num": 1,
  "ref_block_prefix": 4126519930
}
```
可以直接将数据导入MongoDB  

```
#!/usr/bin/env python3
# coding:utf-8

import requests
import json
from pymongo import MongoClient

eos= MongoClient('127.0.0.1', 27017).eos.eos
url = 'http://127.0.0.1:8888/v1/chain/get_block'
blockid = 1
while True:
    print(blockid)
    payload = {'block_num_or_id': blockid, }
    r = requests.post(url, data=json.dumps(payload), timeout=20)
    j = json.loads(r.text)
    eos.insert(j)
    blockid += 1
    if blockid > 200000:
        break
```
导入完成后，建立索引  
db.eos.ensureIndex({"block_num": 1},{unique: true})
db.eos.ensureIndex({"transactions.trx.transaction.actions.name": 1})
...

比如查询EOS主网发行了哪些代币  
这里假设使用的是eosio.token合约  
包含create、issue、transfer方法  
data里包含maximum_supply  

```
#!/usr/bin/env python3
# coding:utf-8

from pymongo import MongoClient

eos = MongoClient('127.0.0.1', 27017).eos.eos
q = eos.find({"transactions.trx.transaction.actions.name":"create"})
cnt = 0
for x in q:
    for t in x['transactions']:
        try:
            for a in t['trx']['transaction']['actions']:
                if a['name'] == 'create':
                    print(x['block_num'])
                    print(a['account'])
                    print(a['data']['maximum_supply'])
                    print('')
                    cnt += 1
        except Exception as e:
            pass
print(cnt)
```
还可以进行更多复杂的查询  
比如账号、转账、合约、资源等  
