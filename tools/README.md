# share-tools.md

## mockservice
> 构造数据服务

### 安装

    npm install mockservice
    
### 依赖

    var ms = require('mockservice');


### 配置


    ms.config({
        name: 'nirvana',
        dir: './nirvana-workspace/nirvana/debug'
    });
    
    ms.config({
         name: 'phoenix',
         dir: './nirvana-workspace/phoenix/debug'
    });
    
    ms.config({
        name: 'innovation',
        dir: './innovation-workspace/innovation/debug'
    });
    
    ms.config({
         name: 'chunhua',
         dir: './chunhua-workspace/chunhua/debug/'
    });

### 构造

    define(function (require, exports, module) {
        var random = require('random');
        var template = require('template');
        var moment = require('moment');
        var memset = require('memset');
        var storage = require('storage');
        var tpl = require('lib/tpl');
        var bizList = require('lib/bizList');
        
        module.exports = function (path, params) {
            var wordSource = ['关键词', '计划', '账户', '单元'];
            return {
                data: random.words(30, wordSource)
                status: 200,
            }
        };
    });





    
-------------

# epipe
> 灵活小巧可扩展的web联调、检测工具

## 安装

```sh
    > npm install epipe -g
```

## 配置
> 使用任何一种方式设置`目标机器`到`本地代理`

- pac代理
- proxySwitch插件
- 系统设置方式

## 使用

```sh
    epipe port=8189 mod=fengchao conser
```

**建议增加alias**

```
    alias pipefc=`epipe port=8189 mod=fengchao conser`
```

**常用命令**

```js
    debug [true/false] // 切换联调/非联调方式
    showlog [true/false] // 显示/隐藏访问log
    moc [path] // 联调模式下,开启本地moc请求
    info // 显示配置信息
```

## 扩展功能
```
> 自定义规则
> 增加请求监控
> 请求拦截，http信息分析
```

--------------------

### asd

辅助系统开发 ( assist system development )

## Feature

- `自动`生成`批量`模块所需文件
- 按`规范`生成脚手架文件
- ----
- 支持`自定义`文件模板
- 支持`多级目录级联`创建
- 支持内建命令扩展
- 支持系统级命令
- 支持自定义上下文
- 支持命令扩展
- 支持`bcs云端`文件备份

## 安装

> npm install asd -g

## 使用

***设置项目基本配置***

``` shell
> asd set email liu@liandong.org # author 信息
> asd set username "Liandong Liu"  # author 信息
> asd set module-files "Action Model View monitor template.tpl style.less"
# 指定mvc需要的文件(有默认配置)
```

**批量生成模块文件**

> 在项目目录中创建指定模块
> 自动会以src/为基准路径配置tpl/less/js中的moduleID, DomId等信息

```shell
> asd set title "看排名"
> asd module src/module/app/coreword ## 创建MVC所需所有文件
```

- 创建单个或多个指定文件

```shell
> asd touch view.js ## 创建单个文件
> asd touch demo/actionConf.js launcher.js 
```

### 云端备份

- 要使用云端备份功能，需要先申请bcs存储
- fcfe可提供公用bucket
- 使用bcs暂时只支持以下几个命令，后期将加入更多支持

```shell
> asd push module/app/coreword.patch 
    ## 将在云端路径module/app/中增加 coreword.patch文件
    
> asd pull module/app/coreword.patch ## 下载云端指定路径下的文件
> asd dir # 显示bucket下所有文件
```

- 在使用前需要先设置sckey 和ackey

```shell
> asd set sckey xxxxx
> asd set ackey yyyyy
```

### 模板数据
> 模板中的数据通过设置的Context自动获取

#### 需要手动设置的数据
- title 当前模块的中文描述
- username 作者名
- email 邮箱

#### 根据创建路径自动生成的上下文内容

> 如创建路径为 workspace/src/module/app/bidInsight

- moduleId 表示以src为基线的path; 除去去后缀部分； module/app/bidInsight

- moduleName 表示文件模块名; bidInsight

- moduleDomId 用于less; tpl； module_app_bidInsight

- monitorTag 表示监控Tag; module_app_bidinsight (全小写)

### conser 命令说明

- conser 使用简单的文本输入流作为交互式命令
- conser 切词默认按空格切词
- 如果要指定包含空格的值，使用双引号\"包含，比如

> asd set username "Liandong Liu"

<table>
  <tr>
    <th>cmd</th> <th>desc</th> <th>usage</th>
  </tr>
  <tr>
    <td>set</td> <td>设置环境值 </td> <td> set key value</td>
  </tr>
  <tr>
    <td>get</td> <td>获取环境值  </td><td> get key</td>
  </tr>
  <tr>
    <td>delete</td> <td>删除环境值 </td><td> delete key</td>
  </tr>
  <tr>
    <td>dump</td> <td> 打印所有值 </td><td> dump </td>
  </tr>
  <tr>
    <td>touch</td> <td>创建文件  </td><td> touch app/util.js lib.js </td>
  </tr>
  <tr>
    <td>module</td> <td>建立新模块</td><td>  module app/coreword  </td>
  </tr>
  <tr>
    <td>mock</td> <td>生成mock文件</td><td>  mock app/coreword  </td>
  </tr>
  <tr>
    <td>push</td> <td> 上传文件</td><td>  push localfile [remotepath] </td>
  </tr>
  <tr>
    <td>pull</td> <td> 下载文件 </td><td> push remotefile [localpath]  </td>
  </tr>
  <tr>
    <td>dir</td> <td> 列表云端列表 </td><td> dir /  </td>
  </tr>
  <tr>
    <td>cat</td> <td> 显示文件 </td><td>  cat filepath  </td>
  </tr>
  <tr>
    <td>save</td> <td>存储文件 </td><td>  save filename  content  </td>
  </tr>
</table>

