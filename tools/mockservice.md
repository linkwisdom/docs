## mockservice

- [安装](#安装)
- [依赖](#依赖)
- [配置](#配置)
- [构造](#构造)

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
