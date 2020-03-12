## Elasticsearch学习笔记

### 基本概念：

Elastic 本质上是一个分布式数据库，允许多台服务器协同工作，每台服务器可以运行多个 Elastic 实例。

- **Node** : 单个 Elastic 实例称为一个节点（node）
- **cluster**: 一组节点构成一个集群（cluster）



- **Index**: 是单个数据的同义词，Elastic 数据管理的顶层单位就叫做 Index（索引），查找数据的时候，直接查找该索引，Elastic 会索引所有字段。

- **Document** : Index 里面单条的记录称为 Document（文档）。许多条 Document 构成了一个 Index。

  Document 使用 JSON 格式表示，下面是一个例子:

  ```json
  {
    "user": "张三",
    "title": "工程师",
    "desc": "数据库管理"
  }
  ```

- **Type**:  Document 可以分组,它是虚拟的逻辑分组，用来过滤 Document

### 新建和删除Index

- 新建Index： 可以直接向 Elastic 服务器发出 PUT 请求

如：新建一个名叫`weather`的 Index

```bash
$ curl -X PUT 'localhost:9200/weather'
```

- 删除Index

```bash
$ curl -X DELETE 'localhost:9200/weather'
```

### 中文分词设置

使用ik,其他如smartcn

### 数据操作

#### 新增记录：

向指定的/Index/Type发送PUT请求,如： 1代表的是这条记录的id，如果不指定会给个随机字符串

```bash
$ curl -X PUT 'localhost:9200/accounts/person/1' -d '
{
  "user": "张三",
  "title": "工程师",
  "desc": "数据库管理"
}
```

#### 查看记录：

向`/Index/Type/Id`发出 GET 请求，就可以查看这条记录。pretty=true表示易读格式返回

```bash
$ curl 'localhost:9200/accounts/person/1?pretty=true'
```

#### 删除记录：

删除记录就是发出 DELETE 请求。

```bash
$ curl -X DELETE 'localhost:9200/accounts/person/1'
```

#### 更新记录：

更新记录就是使用 PUT 请求，重新发送一次数据。

```bash
$ curl -X PUT 'localhost:9200/accounts/person/1' -d '
{
    "user" : "张三",
    "title" : "工程师",
    "desc" : "数据库管理，软件开发"
}' 

{
  "_index":"accounts",
  "_type":"person",
  "_id":"1",
  "_version":2,
  "result":"updated",
  "_shards":{"total":2,"successful":1,"failed":0},
  "created":false
}
```

### 数据查询

使用 GET 方法，直接请求`/Index/Type/_search`，就会返回所有记录。

### 全文搜索

Elastic 的查询非常特别，使用自己的[查询语法](https://www.elastic.co/guide/en/elasticsearch/reference/5.5/query-dsl.html)，要求 GET 请求带有数据体。

```bash
$ curl 'localhost:9200/accounts/person/_search'  -d '
{
  "query" : { "match" : { "desc" : "软件" }}
}'
```

上面代码使用 [Match 查询](https://www.elastic.co/guide/en/elasticsearch/reference/5.5/query-dsl-match-query.html)，指定的匹配条件是`desc`字段里面包含"软件"这个词。返回结果如下。