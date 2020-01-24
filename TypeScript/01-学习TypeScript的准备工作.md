# 学习TypeScript的准备工作

TypeScript是JavaScript类型的超集，它可以编译成纯JS代码。

TS的诞生不是为了替代JS。TS加入了一些JS没有的特性，比如type字面上的意思，TS加入了类型校验，当然类型是可选的，类型推断让一些类型的注释使你的代码的静态验证有很大的不同。

### 为什么要选择TypeScript

* 类型系统，即使不显式的定义类型，也能够自动做出类型推论
* 可以在编译阶段就发现大部分错误，这总比在运行时候出错好
* 增强了编辑器和 IDE 的功能，包括代码补全、接口提示、跳转到定义、重构等

### 安装

```ts
npm install -g typescript
```

### 转换

使用tsc + 文件名称 的方式将TS转换为JS文件。

🌰 tsc app.ts（app.ts为文件名）

### 自动转换

我们可是使用 tsc --init去生成TS配置文件，然后通过tsc命令将所有的TS文件转换为JS文件。

### 通过插件转换

我们可以在vscode通过安装TypeScript Auto Compiler进行转换，省去了我们手动转换的操作。