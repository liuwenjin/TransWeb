# JS小程序引擎——Transweb

## 介绍

Transweb是一个JS小程序引擎。

这个引擎主要有3个目的。

1. 帮助开发人员直接用javascript语言(简称JS)编写能运行在浏览器上的小程序。

2. 让这样的小程序可以自由组合成为功能复杂的程序。

3. 为这些小程序快速生成数据持久化层的数据接口。

为了这三个目的，该小程序引擎具备两个方面的功能： 

1) JS程序控制器功能，负责渲染JS小程序和组合JS小程序；

2) 数据接口生成器功能，可以生成数据库操作接口和自定义数据接口。

## 引擎环境部署和运行

1. 下载并安装nodejs。

2. 下载或clone项目代码。

下载地址: https://github.com/liuwenjin/transweb/archive/master.zip (下载后需解压)

或使用clone地址: liuwenjin/transweb

3. 在控制台打开项目文件目录，运行node webServer.js 命令。

## JS小程序入门

1. 打开项目中static/view目录。

2. 创建一个空白的js文件helloword.js。(将一个空白的text文件后缀名改为js)

3. 在js文件中便在如下代码并保存, 这样就编写了一个js小程序。

```
transweb_cn({
    task: {
        template: '<div>Hello world!</div>',
    }
})
```
这个小程序可以在浏览器地址栏输入localhost:8686?url=view/helloword.js，再按回车运行。

## 数据接口生成

通过配置项目文件目录interface下到index.js并重启webServer，就能自动生成对所配置数据库(当下支持mongodb)记录的增删改查的数据接口。

如下所示为配置interface目录下index.js的代码示例。

```
const config = {
    mongodb: {
        test: {
            host: "localhost",
            port: "27017",
            type: "mongo",
            dbName: "test"
        },
        abc: {
            host: "localhost",
            port: "27017",
            type: "mongo",
            dbName: "abc"
        }
    }
}
module.exports = config;

```


根据上面示例配置代码可以生成对两个mongo数据库的任意集合进行增删改查。

接口地址分别为"/test/xxxx"和"/abc/xxxx"。

test和abc是示例中mongodb配置项属性名称，xxxx为对应数据库的集合名称

现在以test配置项为例简单说明这个配置项生成对test数据库名下的集合进行增删改查的数据接口。

通过这个配置项可以对配置项中对应mongodb的test数据库里的任意一个集合进行增删改查。

对某个集合的增删改查使用同样的url，四种http请求方式分别对应了某个集合的增删改查操作。(实际请求时会根据具体操作需要传递相应的操作参数)

| 操作接口名称 | 请求方式    | 请求参数  | 参数示例  |
|-------|:---:|:-------:|:-----------|
| 查询记录文档  | GET | condition     | { name: "zhangshan"} |
| 新增记录文档 | PUT | data      | { name: "zhangshan", age: 24, position: "teacher" } |
| 更新记录文档  | POST   | set, condition | { name: "zhangshan" }, { id: "23423423242"}    |
| 删除记录文档  | DELETE   | condition | { id: "23423423242"} |

当对某个数据库的集合进行操作时，该数据库和集合不需要提前创建。

操作某个数据库的集合时，若没有数据库或集合，新增文档记录操作会自动创建它们。

## JS小程序开发说明目录

1. [JS小程序的代码结构](liuwenjin/transweb)

2. [JS小程序的组合方式](https://github.com/liuwenjin/transweb/wiki/JS%E5%B0%8F%E7%A8%8B%E5%BA%8F%E7%9A%84%E7%BB%84%E5%90%88%E6%96%B9%E5%BC%8F)

3. [JS小程序的生命周期](https://github.com/liuwenjin/transweb/wiki/JS%E5%B0%8F%E7%A8%8B%E5%BA%8F%E7%9A%84%E7%94%9F%E5%91%BD%E5%91%A8%E6%9C%9F)

4. [JS小程序的接口调用](liuwenjin/transweb)

5. [JS小程序的公用api](liuwenjin/transweb)
