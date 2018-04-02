---
title: npm命令
tags:
  - npm
categories:
  - npm
abbrlink: 90f8805
date: 2018-03-30 17:38:39
---


### 一、命令大全
[命令行api，快戳我](https://docs.npmjs.com/#cli)

* npm list [-g] 查看所有[**全局安装**]的模块
    * (ls、la & ll 可以用作 list 的别名)
    * npm list –depth=0 [-g] 查看[全局]安装的包

* npm list grunt  查看某个模块的版本号
* npm uninstall express 卸载express模块。
* npm update express 更新某个模块
* npm info express 可以查看到express在npm上**发布过哪些版本**
    * npm info react
    * npm show react
    * npm v react
    * https://registry.npmjs.org/react 这些都能得到某个模块的详细信息
    * https://registry.npmjs.org/react/v0.14.6 获得某个模块的某个版本的详细信息
* npm dist-tags ls express 可以查看到express在npm上**发布的最新版本**
* npm outdated express express模块是否**已过时**
* npm root (-g) 查看当前包，全局包的安装路径
* npm config 管理**npm的配置路径**
    * npm config set proxy http://proxy.example.com:8080 npm设置代理
    * npm config get proxy 查看proxy
    * npm config delete proxy 删除proxy
    * npm config list 查看所有配置
* npm view moudleName dependencies 查看包的**依赖关系**
* npm install <packageName> --force 强制**重新安装**某个模块


### 二、npm 缓存
* npm config get cache 获得缓存的目录
对于一些不是很关键的操作（比如npm search或npm view），npm会先查看.cache.json里面的模块最近更新时间，跟当前时间的差距，是不是在**可接受的范围之内**。如果是的，就不再向远程仓库发出请求，而是直接返回.cache.json的数据

### 三、npm 安装模块的过程
1. 发出npm install命令
2. npm 向 registry 查询模块压缩包的网址
3. 下载压缩包，存放在~/.npm目录
4. 解压压缩包到当前项目的node_modules目录

### 四、npm安装不同版本
1. npm install sax@latest
2. npm install sax@0.1.1
3. npm install sax@">=0.1.0 <0.2.0"

### 五、包的依赖
* dependencies 依赖
```
"dependencies": {
    "markdown-it": "^8.1.0"
}
/*这个可以说是我们 npm 核心一项内容，依赖管理，这个对象里面的内容就是我们这个项目所依赖的 js 模块包。下面这段代码表示我们依赖了 markdown-it 这个包，版本是 ^8.1.0 ，代表最小依赖版本是 8.1.0 ，如果这个包有更新，那么当我们使用 npm install 命令的时候，npm 会帮我们下载最新的包。当别人引用我们这个包的时候，包内的依赖包也会被下载下来。*/
```
* devDependencies
在我们开发的时候会用到的一些包，只是在开发环境中需要用到，但是在别人引用我们包的时候，不会用到这些内容，放在 devDependencies 的包，在别人引用的时候不会被 npm 下载

* 锁定依赖
(^)字符：npm 通过脱字符(^)来限定所安装模块的主版本号，^1.5.1 允许安装版本号大于 1.5.1 但小于 2.0.0 版本的模块。
(~)字符: 限定模块的次要版本,~1.5.1 允许安装版本号大于 1.5.1 但小于 1.6.0 版本的模块

### 六、npm脚本执行
* "npm run build-js && npm run build-css" 两个命令同时执行

### package.json
1. name: 包的名字，必须是唯一的，由小写英文字母、数字和下划线组成，不能包含空格。
2. description: 包的简要说明。
3. version: 符合语义化版本识别规范的版本字符串。
4. keywords: 关键字数组，通常用于搜索。
5. maintainers: 维护者数组，每个元素要包含 name 、email(可选)、web(可选)字段。
6. contributors: 贡献者数组，格式与 maintainers 相同。包的作者应该是贡献者数组的第一个元素。
7. bugs: 提交 bug 的地址，可以是网址或者电子邮件地址。
8. licenses: 许可证数组，每个元素要包含 type（许可证的名称）和 url（链接到许可证文本的地址）字段。
9. repositories: 仓库托管地址数组，每个元素要包含 type（仓库的类型，如 git）、URL（仓库的地址）和 path（相对于仓库的路径，可选）字段。
10. dependencies: 包的依赖，一个关联数组，由包名称和版本号组成。
