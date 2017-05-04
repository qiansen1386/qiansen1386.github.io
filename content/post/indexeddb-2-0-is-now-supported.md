+++
categories = ["开发", "中文"]
date = "2017-04-26T15:14:31+08:00"
description = ""
tags = ["前端","新闻"]
title = "IndexedDB 2.0 更新了！"

+++

IndexedDB 2.0 is now supported
------------------------------

> IndexedDB 是一个浏览器内置的 NoSQL 底层实现，它允许你存储简单值以及结构化数据。不过即便是在 Mozilla 的手册上 （[IndexedDB - Web API 接口 | MDN](https://developer.mozilla.org/zh-CN/docs/Web/API/IndexedDB_API)）也是推荐使用第三方封装的库而非直接调用这个 API。Hacker News 上更是招来一片有关 API复杂，没有 SQL 功能的抱怨。这也就是为什么截止到 2017 四月 26 日。整个互联网上有关 IndexedDB 2.0 的中文内容是 0（A big flat zero）

IndexedDB 就是一个简单的 NoSQL 实现，你可以在其上自行封装 API，甚至于封装一个 SQL 语法接口也未尝不可。

> 题外话：因为所有 WebSQL 的实现背后都是 SQLite，所以委员会觉得这个提案已经不太可能进行标准化了。对于委员会的人来说，写一个 SQLite 的说明文件当标准，实在没有意义了。标准的价值就在于统筹多个实现，而因为只有一个实现，标准也就没有了价值。喜欢 SQLite 你就用 WebSQL 就行，反正不同实现的背后都是它。

根据 [Chrome 的功能状态日志](https://www.chromestatus.com/feature/5812621622116352) ，2.0 包括以下功能：
* Binary keys（二进制的键，准确讲是 [Arraybuffer](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/ArrayBuffer)、[typed array objects](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/TypedArray)，和
 [DataView](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/DataView) 加索引）
* Object store（对象存储）
* index renaming（索引重命名）
* getKey() on IDBObjectStore
* getPrimaryKey() on IDBIndex

总体上而言是对旧 API 的补完，如果你不了解第一代，建议先把第一代用起来，因为第一代的浏览器支持已经很全面，甚至包括 IE10。而 2.0 的更新对数据库作者们而言更是喜大普奔，解决了一些之前的顽疾。期待有更多基于 IndexedDB 的好库涌现。如果你习惯 Mongo 或者 Firebase 这类 NoSQL 的话，直接用或自己做个简单封装也未尝不可。（不过话说他的 API 真的是炒鸡强大也炒鸡复杂）

> ####   Mozilla 开发博客的[博文][1]摘要
##### Setters to `IDBObjectStore.name` and `IDBIndex.name`
之前版本的 Index 你可以增减对象存储或索引的方式来升级数据架构，但是并不能重命名。基本上，这意味着你永远没法准确命名，因为随着时间的推移，很多东西的内在含义都可能会发生变化。而现在可以对数据库架构进行更好地升级修改：

```js
let request = indexedDB.open("messageDB", 2);
request.onupgradeneeded = (event) => {
  let txn = event.target.transaction;
  let store = txn.objectStore("text messages");

  store.name = "mobile messages";
  let index = store.index("recipient");
  index.name = "recipients";
};
```
> #####`IDBDatabase.onclose()`
新加了一个数据库的生命周期钩子 `close`。

```js
let request = indexedDB.open("bookstore");
request.onsuccess = (event) => {
  let db = event.target.result;

  db.onclose = (event) => {
    alert("the database: " + db.name + "was closed outside the script!");
  };
};
```
> 。。。 更多内容请[参考原文（En）][1]

#### 浏览器支持

Firefox 51，Chrome 58，Opera release 45

#### 结语

有鉴于 Chrome 58 的开发公告中，着重提到了 IndexedDB 2.0 这里就简单解释下:**是什么**和**为了什么**。目的是为了帮助你了解这个规范背后的逻辑，或者你就当个新闻看也成。至于怎么用，请自行参考 MDN 的手册，或者去 [github 上搜索 indexedDB Wrapper](https://github.com/search?utf8=%E2%9C%93&q=indexedDB+Wrapper)。我因为还没有重度使用过它就不献丑了。

#### Ref: 

- [\[0\]  What’s new in IndexedDB 2.0? ★ Mozilla Hacks（原文）](https://hacks.mozilla.org/2016/10/whats-new-in-indexeddb-2-0/)
- [\[1\] What’s new in IndexedDB 2.0? | Hacker News（上文的吐槽）][1]
- [\[2\]  Indexed Database API 2.0 - Editor’s Draft, 21 April 2017](https://w3c.github.io/IndexedDB/)

[1]: https://news.ycombinator.com/item?id=12793996 "\[1\] What’s new in IndexedDB 2.0? | Hacker News（上文的吐槽）"(https://news.ycombinator.com/item?id=12793996)