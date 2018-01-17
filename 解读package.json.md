###### 1.作用：
每个项目的根目录下面，一般都有一个package.json文件，定义了这个项目所需要的各种模块，以及项目的配置信息（比如名称、版本、许可证等元数据）。npm install命令根据这个配置文件，自动下载所需的模块，也就是配置项目所需的运行和开发环境。

###### 2.指定版本语法：
- 指定版本：比如1.2.2，遵循“大版本.次要版本.小版本”的格式规定，安装时只安装指定版本。
- 波浪号（tilde）+指定版本：比如~1.2.2，表示安装1.2.x的最新版本（不低于1.2.2），但是不安装1.3.x，也就是说安装时不改变大版本号和次要版本号。
- 插入号（caret）+指定版本：比如ˆ1.2.2，表示安装1.x.x的最新版本（不低于1.2.2），但是不安装2.x.x，也就是说安装时不改变大版本号。需要注意的是，如果大版本号为0，则插入号的行为与波浪号相同，这是因为此时处于开发阶段，即使是次要版本号变动，也可能带来程序的不兼容。
- latest：安装最新版本。

>package.json文件可以手工编写，也可以使用npm init命令自动生成。

>tips：这个命令采用互动方式，要求用户回答一些问题，然后在当前目录生成一个基本的package.json文件。所有问题之中，只有项目名称（name）和项目版本（version）是必填的，其他都是选填的。

###### 3.如果一个模块不在package.json：
如果一个模块不在package.json文件之中，可以单独安装这个模块，并使用相应的参数，将其写入package.json文件之中。


```
$ npm install express --save
$ npm install express --save-dev
```
解释：上面代码表示单独安装express模块，--save参数表示将该模块写入dependencies属性，--save-dev表示将该模块写入devDependencies属性。


```javascript
{ 
  <!--项目名称-->
  "name": "boss",
  <!--项目版本-->
  "version": "1.0.0",
  <!--项目描述-->
  "description": "运营管理系统",
  <!--main字段指定了加载的入口文件，require('moduleName')就会加载这个文件。这个字段的默认值是模块根目录下面的index.js。-->
  "main": "server.js",
  <!--scripts指定了运行脚本命令的npm命令行缩写-->
  "scripts": {
    "build": "NODE_ENV=production webpack --config webpack-build-config.js",
    "start": "set NODE_ENV=development && node server",
    "test": "karma start",
    "test-e2e": "protractor protractor.conf.js",
    "update-webdriver": "webdriver-manager update"
  },
  "author": "数云",
  <!--dependencies字段指定了项目运行所依赖的模块-->
  "dependencies": {
    "angular": "1.5.8",
    "angular-cookies": "1.5.8",
    "angular-es-utils": "^1.2.19",
    "angular-resource": "1.5.8",
    "angular-ui-router": "^0.2.18",
    "ccms-components": "^2.24.0",
    "echarts": "^3.8.5",
    "normalize.css": "^3.0.3"
  },
  <!--devDependencies指定项目开发所需要的模块。-->
  "devDependencies": {
    "angular-mocks": "^1.6.8",
    "autoprefixer": "^6.3.6",
    "babel-cli": "^6.26.0",
    "babel-core": "^6.26.0",
    "babel-eslint": "^6.0.4",
    "babel-loader": "^6.2.4",
    "babel-plugin-transform-decorators-legacy": "^1.3.4",
    "babel-preset-es2015": "^6.9.0",
    "babel-preset-stage-0": "^6.5.0",
    "body-parser": "^1.18.2",
    "chokidar": "^1.4.3",
    "clean-webpack-plugin": "^0.1.17",
    "cookie-parser": "^1.4.1",
    "css-loader": "^0.23.1",
    "eslint": "^2.4.0",
    "eslint-config-angular": "^0.5.0",
    "eslint-friendly-formatter": "^1.2.2",
    "eslint-loader": "^1.3.0",
    "eslint-plugin-angular": "^1.0.0",
    "express": "^4.16.2",
    "extract-text-webpack-plugin": "^1.0.1",
    "file-loader": "^0.8.5",
    "html-loader": "^0.4.3",
    "html-webpack-plugin": "^2.30.1",
    "image-webpack-loader": "^1.6.3",
    "jasmine-core": "^2.8.0",
    "json-mock-kuitos": "^1.1.2",
    "karma": "^0.13.22",
    "karma-chrome-launcher": "^0.2.2",
    "karma-jasmine": "^0.3.7",
    "karma-phantomjs2-launcher": "^0.5.0",
    "karma-webpack": "^1.7.0",
    "ng-annotate-loader": "^0.1.0",
    "node-sass": "^3.7.0",
    "phantomjs-prebuilt": "^2.1.16",
    "postcss-loader": "^0.9.1",
    "protractor": "^3.3.0",
    "resolve-url-loader": "^1.4.3",
    "sass-loader": "^3.2.0",
    "style-loader": "^0.13.0",
    "url-loader": "^0.5.7",
    "webpack": "^1.12.14",
    "webpack-dev-middleware": "^1.12.2",
    "webpack-hot-middleware": "^2.21.0"
  }
}

```
其他更多使用介绍请参考[这里](http://javascript.ruanyifeng.com/nodejs/packagejson.html)