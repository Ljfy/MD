### webpack

开发依赖：`*./src/index.js -o ./build/built.js --mode=development* `

生产依赖：`*./src/index.js -o ./build/built.js --mode=production*`

结论：

- 能处理js/json文件，不能处理css/img等等其他资源

- 生产环境比开发环境多一个压缩代码
- 生产环境和开发环境将ES6模块化编译成浏览器识别的模块化

打包css文件

首先通过	` entry:'./src/index.js',`会分析内部依赖图，会发现`index.js引入了 css文件`

在loader解析

