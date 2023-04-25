### npm 笔记
---
 想要使用 `npm` 包管理工具，必须安装 `node`。
#### node 下载与安装
官网地址 https://nodejs.org 
我们直接去官网下载`node`，这种是是最简单的方式，但是更多时候，我们的电脑上需要多个版本的`node`，这种如何解决呢？这个时候`nvm`就派上用场了。
##### nvm 管理 node 版本
下载地址：https://github.com/coreybutler/nvm-windows/releases
建议下载安装版 安装完成后，在命令行中输入 `nvm -v` 测试一下，是否安装成功
##### nvm 常用的命令：
- nvm -v  查看版本号
- nvm ls 查看安装的 `node`
- nvm ls available 可安装的 `node` 版本
- nvm install [版本号] 安装node
- nvm use [版本号] 使用某个版本的`node`
- nvm uninstall [版本号] 下载`node`

node安装好了后，就可以使用npm了。直接使用npm很多时候，下载依赖库很慢，或者下载不了。这时候我们就需要使用镜像了
 ### 镜像问题
 有两种解决方案：
 - 手动切换镜像
 - 通过`nrm`切换镜像
 #### 手动切换镜像
 ~~~
 npm config set registry [镜像地址] 
 eg： 
    npm config set registry https://registry.npmmirror.com/
 ~~~

#### 通过nrm切换镜像
`nrm` 地址：https://www.npmjs.com/package/nrm

安装`nrm`  `npm install nrm -g` , 这是全局安装（一般情况下像这种工具类的，都是全局安装）。安装完成后检测是否安装成功`nrm --version` or `nrm -V` （注意是大写的V）
常用的 `nrm` 命令：
- `nrm ls` 查看维护的镜像
- `nrm test`    测试延迟
- `nrm use [option]` 指定使用哪个镜像

上述前置工作完成后，接下来我们就可以了解以下 `npm` 常用的命令了。
#### npm 常用命令
##### `npm` 文档地址： https://www.npmjs.cn/ 
##### `npm init`
初始化npm工程
~~~
npm init      需要回答很多问题
npm init -y   不用回答任何问题
~~~

##### `npm config`
查看配置
~~~
npm config list
npm config get [key]
npm config set [key] [value]
npm config delete [key]
~~~

##### `npm install`
下载依赖
~~~
下载某个版本或者某个tag的依赖包  [options] 有可能是 --save-dev， -g 等等，具体查看文档就行 --save-dev 代表开发阶段依赖包，-g 代表全局安装

npm install <name> [options]
npm install <name>@<version> [options]
npm install <name>@<tag> [options]
~~~
##### `npm uninstall`
下载依赖包
~~~
npm uninstall <name>
~~~














