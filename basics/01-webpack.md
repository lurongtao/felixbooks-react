# webpack

*webpack* 是一个现代 JavaScript 应用程序的*静态模块打包器(module bundler)*。当 webpack 处理应用程序时，它会递归地构建一个*依赖关系图(dependency graph)*，其中包含应用程序需要的每个模块，然后将所有这些模块打包成一个或多个 *bundle*

其它相似打包工具还有[rollup.js](<https://www.rollupjs.com/guide/zh>) 、 [parcel](<https://parceljs.org/>)、[FIS](<http://fis.baidu.com/>)等


按照[webpack的指南](<https://www.webpackjs.com/guides/>)**(注意是指南不是概念不是api)**进行针对性的讲解即可，需要被充一下工程化的知识


## 工程化

这个部分的内容可以做为一些思想给学员讲解，不需要学员掌握。可以理解为扩展的内容

### 什么是JS项目工程化

- 版本控制
- 自动化持续继承、持续交付(CI/CD)
- 代码质量控制(QA)
- 工具
- 模块化
- 文档
- demo

### 编译过程

自动化处理每次push, tag, release的任务队列

1. 安装
   - 安装 : npm命令行工具
   - 安全审计：npm audit
2. Lint 
   - 格式检查: eslint/stylelint
   - 格式化: prettier
3. 测试
   - 测试套装: jest / mocha / ava / kamar
   - 代码覆盖量: nyc / codecov / coveralls
4. 构建
   - 转换器: babel / TS / flow
   - 预处理器: sass / less / postcss
   - 代码混淆: uglify-js / terser
   - 打包及tree shaking: webpack / rollup / parcel
   - 压缩(gzip等)
   - 复制 / 删除 / 移动文件
   - 检查打包文件的大小
   - 移除无用的代码
5. push
   - 交付:  git 
   - 发布: npm
6. 部署
   - 服务器
     - Pages: git pages
     - 云服务器: aliyun / qcloud / aws
7. Story Book

## create-react-app

全局安装create-react-app

```sh
$ npm install -g create-react-app
```

创建一个项目

```sh
$ create-react-app your-app 注意命名方式

Creating a new React app in /dir/your-app.

Installing packages. This might take a couple of minutes. 安装过程较慢，可以推荐学员使用yarn
Installing react, react-dom, and react-scripts... 
```

如果不想全局安装，可以直接使用npx

```sh
$ npx create-react-app your-app	也可以实现相同的效果
```


这需要等待一段时间，这个过程实际上会安装三个东西

- react:  react的顶级库
- react-dom: 因为react有很多的运行环境，比如app端的react-native, 我们要在web上运行就使用react-dom
- react-scripts: 包含运行和打包react应用程序的所有脚本及配置

出现下面的界面，表示创建项目成功:

```sh
Success! Created your-app at /dir/your-app
Inside that directory, you can run several commands:

  npm start
    Starts the development server.

  npm run build
    Bundles the app into static files for production.

  npm test
    Starts the test runner.

  npm run eject
    Removes this tool and copies build dependencies, configuration files
    and scripts into the app directory. If you do this, you can’t go back!

We suggest that you begin by typing:

  cd your-app
  npm start

Happy hacking!
```

根据上面的提示，通过`cd your-app`命令进入目录并运行`npm start`即可运行项目。

生成项目的目录结构如下：

```sh
├── README.md							使用方法的文档
├── node_modules					所有的依赖安装的目录
├── package-lock.json			锁定安装时的包的版本号,保证团队的依赖能保证一致。
├── package.json					
├── public								静态公共目录
└── src										开发用的源代码目录
```



常见问题：

- npm安装失败
  - 切换为npm镜像为淘宝镜像
  - 使用yarn，如果本来使用yarn还要失败，还得把yarn的源切换到国内
  - 如果还没有办法解决，请删除node_modules及package-lock.json然后重新执行`npm install命令`
  - 再不能解决就删除node_modules及package-lock.json的同时清除npm缓存`npm cache clean --force`之后再执行`npm install`命令