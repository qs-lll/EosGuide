##### EOS同步主网并拉取交易记录
1. 修改config.ini
	
	配置文件位置:
	
	```
	linux-ubuntu:  ~/.local/share/eosio/nodeos/config/  
mac-osx:  ~/Library/Application\ Support/eosio/nodeos/data/confi  
	```
	1. 添加peer
		
		<a href="https://eosnodes.privex.io/?config=1">https://eosnodes.privex.io/?config=1</a>
		
		复制内容 添加到config.ini底部
		
	2. 修改config.ini公链本地db大小
	
		```
		 chain-state-db-size-mb = 40240.
		```
2. genesis.json

	在config目录下创建genesis.json文件
		
	```
	{  
  	"initial_timestamp": "2018-06-08T08:08:08.888",  
  	"initial_key": "EOS7EarnUhcyYqmdnPon8rm7mBCTnBoot6o7fE2WzjvEX2TdggbL3",  
  	"initial_configuration": {  
    	"max_block_net_usage": 1048576,  
    	"target_block_net_usage_pct": 1000,  
    	"max_transaction_net_usage": 524288,  
    	"base_per_transaction_net_usage": 12,  
    	"net_usage_leeway": 500,  
    	"context_free_discount_net_usage_num": 20,  
    	"context_free_discount_net_usage_den": 100,  
    	"max_block_cpu_usage": 200000,  
    	"target_block_cpu_usage_pct": 1000,  
    	"max_transaction_cpu_usage": 150000,  
    	"min_transaction_cpu_usage": 100,  
    	"max_transaction_lifetime": 3600,  
    	"deferred_trx_expiration_window": 600,  
    	"max_transaction_delay": 3888000,  
    	"max_inline_action_size": 4096,  
    	"max_inline_action_depth": 4,  
    	"max_authority_depth": 6  
  	}  
	}  
	```
	
2. 启用节点同步主网节点
	
	首次执行:
	```
	nodeos eosio --plugin eosio::chain_api_plugin --plugin eosio::history_api_plugin --contracts-console --filter-on "*" --genesis-json genesis.json
	```
	
	手动取消后执行
	```
	nodeos eosio --plugin eosio::chain_api_plugin --plugin eosio::history_api_plugin --contracts-console --filter-on "*" 
	```
	
	抛出异常后重置执行**会导致数据重新进行同步**
	```
	nodeos eosio --plugin eosio::chain_api_plugin --plugin eosio::history_api_plugin --contracts-console --filter-on "*" --genesis-json genesis.json --delete-all-blocks
	```
3. 测试当前网络
	
3. get_info获取当前状态
	
	```
	./cleos get info
	```
	或
	
	```
	http://127.0.0.1:8888/v1/chain/get_info
	```
	
	
	
	
	
	
	
	
	
	
	
	
	
	
	一切顺利的话,chain_id是:
	
	```
	"chain_id": "aca376f206b8fc25a6ed44dbdc66547c36c6c33e3a119ffbeaef943642f0e906"
	```
	
	```
	{
    "server_version": "79651199",
    "chain_id": "aca376f206b8fc25a6ed44dbdc66547c36c6c33e3a119ffbeaef943642f0e906",
    "head_block_num": 328455,
    "last_irreversible_block_num": 328454,
    "last_irreversible_block_id": "00050306b2d3e6e247d5021520489e3a3b876c424fd567a14ae69b95f362da01",
    "head_block_id": "00050307f3bb2820b33ff9d0a2957de6345e098df69737e36c9d5786cdbe281d",
    "head_block_time": "2018-06-12T08:35:16.500",
    "head_block_producer": "genesisblock",
    "virtual_block_cpu_limit": 200000000,
    "virtual_block_net_limit": 1048576000,
    "block_cpu_limit": 199900,
    "block_net_limit": 1048576
}
	```
3. 获取账号交易记录

	```
	./cleos get actions eosio
	```
	>我是图片
	
4. 获取交易信息

	```
	./cleos get transaction eb4b94b72718a369af09eb2e7885b3f494dd1d8a20278a6634611d5edd76b703
	```
	>我也是图片
5. 安全停止nodeos
	```
	This appears to be two different issues.

Startup after a crash or ungraceful shutdown nearly always fails due to corruption of the boost shared memory cache of the in-memory database. --resync is required to clean up the mess.

For normal shutdown, never kill with -9. Always use either the default (no argument) signal (which is SIGTERM) or SIGINT. Numerically, those are 15 and 2, respectively.

pkill nodeos | Safe
pkill -15 nodeos | Safe
pkill -2 nodeos | Safe
pkill -TERM nodeos | Safe
pkill -SIGTERM nodeos | Safe
pkill -INT nodeos | Safe
pkill -SIGINT nodeos | Safe
pkill -9 nodeos | Not Safe
pkill -KILL nodeos | Not Safe
pkill -SIGKILL nodeos | Not Safe

The core dump is a different problem. That looks like a corrupted network packet, specifically a signed_block_summary. Summary messages are being eliminated from the protocol, so this particular error will no longer be possible soon.
	```
