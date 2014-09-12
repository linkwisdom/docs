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
