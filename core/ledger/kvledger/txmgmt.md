#### txmgmt

##### validateTx(txRWSet, updates)

参数注释：txRWSet交易模拟结果/读写集，updates账本更新（顺序校验一个区块中的交易，每成功验证一个交易，就把交易的写集放进去）
* 该校验只校验读写集中的读集以及范围查询，不做写集的校验（不需要）。
* 针对读集，就是对于每一个Key检查是否在updates中存在，如果有，验证就不成功，另外还要检查当前账本（截至上一个区块）中它的version是否跟读集（背书节点模拟时）中的version一致，因为交易受orderer排序影响以及网络延迟影响，检查version是保证该交易之前没有交易变更过要读的Key，保证信息读取的准确性。
* 针对范围查询，就是在现有账本状态（截至上一个区块）+update中重新执行范围查询，比对结果是否还是一样。
