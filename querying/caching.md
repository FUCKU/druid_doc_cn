# 查询缓存

Druid通过LRU缓存支持查询结果缓存。结果以每个段为基础存储，并与给定查询的参数一起存储。这允许Druid部分地基于高速缓存中的分段结果返回最终结果，并且部分地基于扫描历史/实时段的分段结果。

段结果可以存储在本地堆缓存或外部分布式键/值存储中。可以在Historical和Broker级别启用段查询高速缓存（不建议在两者上启用高速缓存）。

## 查询经纪人缓存

与在小型群集的历史记录上启用查询缓存相比，在代理上启用缓存可以产生更快的结果。这是较小生产群集（<20台服务器）的推荐设置。请注意，在Broker上启用缓存时，将根据每个段返回Historicals的结果，并且Historicals将无法执行任何本地结果合并。

## 查询历史记录缓存

较大的生产群集应仅在历史记录上启用缓存，以避免必须使用代理来合并所有查询结果。在历史记录而不是经纪人上启用缓存使历史记录能够自己进行本地结果合并，并减少对经纪人的压力。