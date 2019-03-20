# MongoDB

- NoSQL: Not Only SQL 非关系型数据库
- 内存级读写（毫秒级）

## Introduction MongoDB

### 为什么出现NoSQL

> 随着访问量的上升，网站的数据库性能出现问题

### 优点

- 高可扩展性
- 分布式计算
- 低成本
- 架构的灵活性，半结构化数据
- 没有复杂的关系

### 缺点

- 没有标准化
- 有限查询功能

### 分类

- 列存储：Hbase, Cassndra, Hypertable
- 文档存储：MongoDB, CouchDB
- key-value存储：Tokyo Cabinet /Tyrant, Berkeley DB, MemcacheDB
- 图存储：Neo4J, FlockDB
- 对象存储：db4o, Versant
- xml数据库：Berkeley DB XML, BaseX

## 用户浏览过程

- user -> application ->redis/mongodb -> mysql

### What [MongoDB](https://mongodb.com)

> 分布式文档存储的NoSQL数据库

- C++语言编写，运行稳定、性能高
- Web 应用提供可扩展的高性能数据存储解决方案

## MongoDB Features

- 模式自由：不同结构的文档存储在同一个数据库里
- 面向集合的存储：适合存储 JSON 风格文件的形式
- 完整的索引支持：对任何属性可索引
- 复制和高可用性：支持主从撇脂
- 自动分片
- 丰富的查询
- 快速的更新
- 高效的传统存储方式：支持二进制数据及大型对象（图片等）

## 名词对比

- 解释/SQL/MongoDB
- 数据库/database/database
- 表, 集合/table/collection
- 记录,文档/row/document
- 字段, 域或键/column/field/key
- 索引/index/index
- 表连接/join/无
- 主键/primary key/primary key

- 三元素：数据库/集合/文档
  - 集合就是关系数据库中的表，存储多个文档
  - 文档对应着关系数据库中的行
  - 文档，就是一个对象，有键值对构成，是json的扩展BSON形式

## 下载安装 MongoDB

### Windows 下安装

注意：安装之前建立一个目录用于存储**mongodb的数据**

1. 启动服务（指定数据安装目录）`E:\usr_local\mongodb\bin\mongod.exe --dbpath E:\usr_local\mongodb\data`
2. 配置环境变量 path: `E:\usr_local\mongodb\bin`
3. 启动数据库服务：修改 **mongodb.bat** 文件

#### mongod服务

mongodb.bat

- 27017端口(原生端口) shell/GUI
- 28017端口(扩展端口) 用于web服务

#### mongod客户端

```bat
mongod --dbpath E:\usr_local\mongodb\data
```

mongo.bat

```bat
mongo 127.0.0.1:27017
```

### 操作数据库流程

```bson
1. 创建数据库（什么都不操作就离开时这个空数据库就会被删除）

use [databasename]
use temp

2. 查看数据库
show dbs 显示 admin/config/local 三个数据库

3. 给指定数据库添加集合并且添加记录
db.persons.insert({name: "wovert"})

集合：persons
记录：{name:wovert}

4. 显示数据库
show dbs

admin   0.000GB
config  0.000GB
local   0.000GB
temp    0.000GB

5. 查看当前数据库中的所有文档

show collections

6. 查询指定文档的数据

查询所有：db.[documentName].find()
查询第一条数据：db.[documentName].fodnOne()

7. 更新文档数据

db.[documentName].update({查询条件}, {$set: {更新内容}})

db.persons.update({name:'wovert'}, {$set: {name: 'wovert.com'}})

var p = db.persons.findOne()
db.persons.update(p, {name: "mew value"})

8. 删除文档数据

db.[documentName].remove({删除条件})

9. 删除库中的集合

10. 删除数据库

11. shell

12. mongoDB API

数据库和集合命令规范


```

## 服务端 mongod

- 开启验证模式
`# mongod -f /etc/mongod.conf --fork --auth`

## 创建用户

```bson
use admin
db.createUser({
  user:'admin',
  pwd:'adminpwd',
  roles:[{role:'userAdminAnyDatabase', db:'admin'}]
})
db.auth('admin','adminpwd')

use test
db.createUser({
  user:'test',
  pwd:'testpwd',
  roles:[{role:'readWrite',db:'test'}]
})
db.auth('test','testpwd')
```

## MongoDB GUI

- [Robo](https://robomongo.org)

## 数据类型

- Object ID：文档ID (12byte 16机制)
  - 4 byte timestamp
  - 3 byte 机器id
  - 2 byte mongodb的服务进程id
  - 3 byte 增量值
- String
- Boolean
- Integer
- Double
- Arrays
- Object
- Null
- Timestamp
- Date

## 数据库操作

- 查看当前数据库：`db`
- 查看所有数据库：`show dbs`
- 切换数据库：`use test` 没有真正创建数据库，而是临时存放在数据库缓存池当中
- 删除当前数据库: `db.dropDatabase()`
- 创建数据库：`use test`
  - `show dbs` 不现实当前数据库

## 集合操作

- create: db.createCollection(name, options)
	+ db.createCollection("stu", {capped:true, size:10})
		* capped 覆盖

- view: show collections
- delete: db.集合名.drop()

## 文档操作

- 插入：
  - db.集合名称.insert({...})
- 查询:
  - db.集合.find()
- 更新：
	+ db.集合.update({条件}, {修改数据})
	+ db.集合.update({name:'hr',{$set:{name:'hys'}}}) $set 不修改文档结构
	+ db.集合.update({name:'hr',{$set:{name:'hys'}}}, {multi:true}) 修改多行，默认修改一行
- 删除：
	+ db.集合.remove({条件}, {justOne:false}) 默认删除所有
	+ db.集合.remove({}) 全部删除


## 查询
- db.集合.find()
- db.集合.find(条件)
- db.集合.find().pretty()
- db.集合.findOne()


## 比较运算符
- 等于
	+ db.stu.find({name:'gj'})
- $lt
- $lte
- $gt
- $gte
	+ db.stu.find({age:{$gte:18}})
- $ne


- $or (大于)
	+ db.stu.find({$or:[{age:{$gt:18}},{gender:1}]})

## 范围运算符
- $in, $nin
- db.stu.find({age:{$in:[18,28]}})

## 正则表达式
- // or $regex
`db.stu.find({name:/^ad/})`
`db.tu.find({name:{$regex:'^ad'}})`

## 自定义查询
`db.stu.find({$where: function(){return this.age>20}})`


## limit
`db.stu.find().limit(2)`

## skip 跳过指定数量
`db.stu.find().skip(2) 第三条开始`

## 投影
`db.stu.find({}, {_id:0,字段名:1,...})`
- 1:显示，0:不显示

## 排序
- 1:升序
- -1:降序
`db.stu.find().sort({字段:1})`


## 统计个数
`db.stu.find(条件).count()`
`db.stu.count({条件})`

## 消除重复
`db.stu.distinct(去重字段, {条件})`

## 聚合 aggregate
`db.stu.aggregate([{管道:{表达式}}])`

- 管道
$group: 集合中的文档分组

- 按gender分组，counter作为计算男生，女生的总人数
`db.stu.aggregate([
	{
		$group:
			{
				_id: '$gender',
				counter: {$sum:1} 或者 {$sum:'$age'}, {$push:'$$ROOT'}
			}
	}
])`


- $match: 过滤数据
age > 20
db.stu.aggregate([
	{$match:{age:{$gt:20}}}
])

- $project: 投影
	+ 结果集中一部分显示
`db.stu.aggregate([
	{
		$group:
			{
				_id: '$gender',
				counter: {$sum:1} 或者 {$sum:'$age'}, {$push:'$$ROOT'}
			}
	},
	{
		$project: {
			_id: 0,
			counter: 1
		}
	}
])`


- $sort:
`db.stu.aggregate([
	{$group:{
				_id: '$gender',
				counter: {$sum:1} 或者 {$sum:'$age'}, {$push:'$$ROOT'}
			}
	},
	{$project: {_id: 0,counter: 1}
	},
	{$sort:{counter:1}}
])`

$limit
$skip

- $unwind: 将数组类型的字段进行拆分
`db.t2.insert({_id:1, title:'t-shirt', size:['M','L','S']})`

`db.t2.aggregate([
	{$unwind:'$size'}
])`


- 表达式
$sum
$avg
$min
$max
$push: 数组
$first
$last

- $$ROOT: 将文档内容加入到结果集的数组中


# explain 性能分析
`db.t1.find().explain('executionStats')`

# 创建索引
`db.t1.ensureIndex({属性:1[,属性:2]})`

db.t1.getIndexes()
db.t1.dropIndexes('索引名称')


# 用户管理
> 角色-用户-数据库的安全管理方式

- 系统角色
	+ root: 只在admin数据库的可用，超级账号/超级权限
	+ Read: 允许用户读取指定数据库
	+ readWrite: 允许用户读写指定数据库


## 创建超级管理员
`use admin
db.createUser({
	user:'admin',
	pwd:'123',
	roles:[{role:'root',db:'admin'}]
})`

- 启用安全认证
sudo vi /etc/mongod.conf
	ecurity:
		authorization: enabled

`$ mongo --help`
`$ mongo -u admin -p 123 --authenticationDatabase admin`
> db
> use admin
> show collections
> db.syste.users.find()
> show users()

- 创建普通用户
`use test
db.createUser({
	user:'test',
	pwd:'123',
	roles:[{role:'readWrite',db:'test'}]
})`


# 复制(副本集)

1. create directory
`$ mkdir {t1,t2}`

2. start mongod
`mongod --help`
`$ mongod --bind_ip 192.168.100.1 --port 12017 --dbpath ~/t1 --replSet rs0`
`$ mongod --bind_ip 192.168.100.1 --port 12017 --dbpath ~/t2 --replSet rs0`


# 手动备份

- 备份
`$ mongodump -u user -p 123 -h host --authenticationDatebase dbname -d dbname -o dbdirectory`

- 恢复
`$ mongorestore -u admin -p 123 -h host  --authenticationDatebase admin -d dbname --dir dbdirectory`
`--dir: 备份数据所在位置`

# py交互
sudo pip install pymongo

