# Nebula Graph {{ nebula.release }} release notes

## 优化

- 支持在表达式中使用模式，如：`MATCH (v:player) WHERE (v)-[:like]->() RETURN v`。[#3997](https://github.com/vesoft-inc/nebula/pull/3997) 
- 支持用`CLEAR SPACE`清除图空间数据并保留 Schema 信息。[#3989](https://github.com/vesoft-inc/nebula/pull/3989) 
- 支持在匹配模式中重复点的别名，如：`MATCH (v)-->(v)`。[#3929](https://github.com/vesoft-inc/nebula/pull/3929) 
- 优化`SUBGRAPH`和`FIND PATH`从而提高性能。[#3871](https://github.com/vesoft-inc/nebula/pull/3871) [#4095](https://github.com/vesoft-inc/nebula/pull/4095) 
- 优化路径以减少冗余路径和时间复杂度。[#4126](https://github.com/vesoft-inc/nebula/pull/4162) 
- 优化获取属性的方式进而优化`MATCH`语句的性能。[#3750](https://github.com/vesoft-inc/nebula/pull/3750) 
- 优化`GO`、`YIELD`子句，减少不必要的属性读取。[#3974](https://github.com/vesoft-inc/nebula/pull/3974) 
- 支持获取属性时 Filter 及`LIMIT`下推。 [#3844](https://github.com/vesoft-inc/nebula/pull/3844) [#3839](https://github.com/vesoft-inc/nebula/pull/3839) 
- 支持`LOOKUP`聚合下推。[#3504](https://github.com/vesoft-inc/nebula/pull/3504) 
- `maxHop`在匹配可变长度路径中是可选的。[#3881](https://github.com/vesoft-inc/nebula/pull/3881) 
- 使用`DROP SPACE`之后图空间将进行物理删除。[#3913](https://github.com/vesoft-inc/nebula/pull/3913) 
- 优化日期时间/日期/时间中数字解析。[#3797](https://github.com/vesoft-inc/nebula/pull/3797) 
- 添加`toSet`函数，将`LIST`或`SET`转换为`SET`。[#3594](https://github.com/vesoft-inc/nebula/pull/3594) 
- 支持使用 nGQL 来显示服务的 HTTP 端口，并禁用 HTTP2 端口。[#3808](https://github.com/vesoft-inc/nebula/pull/3808) 
- 限制单用户、单机器连接数据库的会话数量。[#3729](https://github.com/vesoft-inc/nebula/pull/3729) 
- 优化存储启动时的等待机制，保证与 Meta 服务及时连接。[#3971](https://github.com/vesoft-inc/nebula/pull/3971) 
- 当节点存在多条路径，某条数据路径对应磁盘故障时，不再需要重建整个节点。[#4131](https://github.com/vesoft-inc/nebula/pull/4131)
- 优化 Job 管理。[#3976](https://github.com/vesoft-inc/nebula/pull/3976) [#4045](https://github.com/vesoft-inc/nebula/pull/4045) [#4001](https://github.com/vesoft-inc/nebula/pull/4001)  
- 支持在作业管理中管理`DOWNLOAD`、`INGEST SST`文件。[#3994](https://github.com/vesoft-inc/nebula/pull/3994)
- 支持显示失败作业的错误码。[#4067](https://github.com/vesoft-inc/nebula/pull/4067) 
- 支持禁用 OS 页面缓存，只在共享环境中使用块缓存和 Nebula 存储缓存，以避免应用程序之间的内存占用干扰。[#3890](https://github.com/vesoft-inc/nebula/pull/3890) 
- 更新 KV 分离阈值的默认值（从 0 到 100）。[#3879](https://github.com/vesoft-inc/nebula/pull/3879) 
- 支持 gflag 设置表达式深度上限，方便调整适配不同的机器环境。[#3722](https://github.com/vesoft-inc/nebula/pull/3722) 
- 新增`KILL QUERY`的权限检查。当启用身份验证时，具有 GOD 角色的用户可以终止所有查询，而具有其他角色的用户只能终止自己的查询。[#3896](https://github.com/vesoft-inc/nebula/pull/3896) 
- 新增 distcc、sccache 等编译方式的支持。[#3896](https://github.com/vesoft-inc/nebula/pull/3896) 
- meta dump 工具支持更多可 dump 的表。[#3870](https://github.com/vesoft-inc/nebula/pull/3870) 
- 存储层将写操作（`INSERT VERTEX`或者`INSERT EDGE`）的并发控制，从报错并要求客户端重试，改为内部排队，以便客户端更简单适配。[#3926](https://github.com/vesoft-inc/nebula/pull/3926)

## 缺陷修复

- 修复`LOOKUP`中使用函数调用作为过滤器的一部分导致的服务崩溃问题。[#4111](https://github.com/vesoft-inc/nebula/pull/4111) 
- 修复`IN`表达式中的属性没有索引绑定时的崩溃问题。[#3986](https://github.com/vesoft-inc/nebula/pull/3986) 
- 修复并发扫描点或者边时导致 Storage 服务崩溃的问题。[#4190](https://github.com/vesoft-inc/nebula/pull/4190) 
- 修复`MATCH`语句的聚合子句中，使用模式表达式时崩溃的问题。[#4180](https://github.com/vesoft-inc/nebula/pull/4180) 
- 修复获取`profile`查询的 JSON 结果导致的崩溃问题。[#3998](https://github.com/vesoft-inc/nebula/pull/3998) 
- 修复 Lambda 函数中的`async`接口运行完毕且`threadManager`中的任务未执行时的崩溃问题。[#4000](https://github.com/vesoft-inc/nebula/pull/4000) 
- 修复`GROUP BY`输出的缺陷。[#4128](https://github.com/vesoft-inc/nebula/pull/4128) 
- 修复`SHOW HOSTS`有时不能不显示版本的缺陷。[#4116](https://github.com/vesoft-inc/nebula/pull/4116) 
- 修复`id(n) == $var`，`id(n) IN [$var]`， `id(n) == $var.foo.bar`， `id(n) IN $var.foo.bar`参数化的缺陷。[#4024](https://github.com/vesoft-inc/nebula/pull/4024) 
- 修复`MATCH...WHERE`中出现错误路径方向的缺陷。[#4091](https://github.com/vesoft-inc/nebula/pull/4091) 
- 修复`WHERE`子句同时引用多`MATCH`变量结果显示不正确的缺陷。 [#4143](https://github.com/vesoft-inc/nebula/pull/4143) 
- 修复优化规则的缺陷。[#4146](https://github.com/vesoft-inc/nebula/pull/4146) 
- 修复节点处理 Raft 快照失败的缺陷。[#4019](https://github.com/vesoft-inc/nebula/pull/4019) 
- 修复节点接收快照后无法接受更多日志的缺陷。[#3909]( https://github.com/vesoft-inc/nebula/pull/3909)
- 修复快照中不包含不带 Tag 的点的缺陷。[#4189](https://github.com/vesoft-inc/nebula/pull/4189) 
- 修复同一个 Tag 或者 Edge 的版本超过 255 后读取最新版本的 Schema 失败的缺陷。[#4023](https://github.com/vesoft-inc/nebula/pull/4023) 
- 修复`SHOW STATS`不统计不带 Tag 的点的缺陷。[#3967](https://github.com/vesoft-inc/nebula/pull/3967) 
- 修复有时时间戳获取错误的缺陷。[#3958](https://github.com/vesoft-inc/nebula/pull/3958) 
- 修复可以为`root`用户分配图空间中的其他角色的缺陷。[#3868](https://github.com/vesoft-inc/nebula/pull/3868) 
- 修复词法分析器中的列索引重复计数的缺陷。[#3626](https://github.com/vesoft-inc/nebula/pull/3626) 

## 历史版本

[历史版本](https://nebula-graph.com.cn/tags/release-note/)