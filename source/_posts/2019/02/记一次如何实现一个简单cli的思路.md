---
title: 记一次如何实现一个简单cli的思路
tags:
  - node cli
categories:
  - Nodejs
date: 2019-02-19 23:56:47
---

#### 需求
这几天自己在提取一个技术需求，原始需求是这样：
```
通过一个脚本命令，能够实现将抽象化的模板文件生成为一个项目实体（即一个spa应用对应的node层代码和前端代码），并以最简版方式可运行。
```
#### 思路
依据以往经验，直接在项目结构里加一个script脚本，然后node运行脚本以实现需求。
这次的想法不太一样，考虑到后面可能还会添加其他脚本，dev depedency会对项目的package.json进行污染，其次实现模板功能的话本身模板文件放在项目中就不太合适。最后考虑发一个npm package，实现一个针对于应用仓库的脚本包，在应用仓库内运行cli命令。

其二、希望脚手架工具本身能够有较高的定制性以及一定的健壮性，这样的话避免不了一定的对话交互和检测；

其三、模板并非简单的cp，而是模板目录以及文件内容有一定的灵活性，需要提供placeholder进行内容替换；

依据转换后的需求技术要点，谈谈下面的具体实现。

#### 实现
##### 1. init一个npm仓库
通过husky+commitlint进行commit msg规范
##### 2. package.json配置好bin，以及files
```js
"bin": {
  "run": "bin/index.js"
},
"files": [
  "bin",
  "template"
],
```

bin字段会在上层项目的node_modules/.bin/目录生成一个link到配置的node脚本
files代表发npm包时依然包含哪些目录

##### 3. 编写bin/index.js
编写之前，基本锁定了几个常用的脚本编写依赖工具。
* 实现cli，标定各种命令以及对应参数，可以使用tj大神的`commander`工具
* 交互式对话，选用`inquirer`
* 基于任务实现模板的生成功能，选用`gulp`
* 命令行帮助显示工具`chalk`


```js
#!/usr/bin/env node

const commander = require('commander');
const newPlugin = require('./newPlugin.js');
const pkg = require('../package.json');

commander
  .version(pkg.version, '-v, --version');

commander
  .command('new-plugin')
  .description('新建一个插件')
  .action(newPlugin);

//EXTEND: 添加其他命令,提供cli的可扩展性

commander.parse(process.argv);
```

newPlugin.js
```js
const gulp = require('gulp');
const chalk = require('chalk');
const path = require('path');
const inquirer = require('inquirer');
const fs = require('fs');

const log = console.log;
// outputPath在dev模式下为本仓库的build目录
const outputPath = process.env.NODE_ENV === 'development' ? path.resolve(__dirname, '../build') : process.cwd();

// 注意此处进行gulp的所有task注册
require('./tasks');

module.exports = async function() {
  // 获取已存在的spa目录列表，检测防止重复创建
  let existedPluginNameList = [];
  try {
    existedPluginNameList = fs.readdirSync(path.resolve(outputPath, './app/controllers'));
  } catch (error) {}

  const { pluginName, pluginTitle, mode } = await inquirer.prompt([
    {
      type: 'input',
      name: 'pluginName',
      message: '请输入名称（英）',
      validate: input => {
        if (existedPluginNameList.indexOf(input) > -1) {
          return '该插件已存在，请重新输入';
        }
        return true;
      },
    },
    {
      type: 'input',
      name: 'pluginTitle',
      message: '请输入名称（中）',
      validate: input => input && input.length > 0,
    },
    {
      type: 'list',
      name: 'mode',
      message: '请选择生成模式',
      choices: [
        { name: `Simple: ${chalk.bgRed("只生成必要的目录及文件")}`, value: 'simple'},
        { name: `Default: ${chalk.bgRed("包含列表页、创建页、成功页等")}`, value: 'default'}
      ],
      default: 'default'
    },
  ]);

  log('名称: ', chalk.green(`${pluginTitle}`));
  log('outputPath: ', chalk.green(outputPath));
  log(chalk.yellow('开始初始化 \n'));
  // 此处在gulp上挂载一个私有属性customParams供task中运行时调用，免去传参
  gulp.customParams = {
    outputPath,
    pluginName,
    pluginTitle,
  }
  gulp.task('default')(err => { log(chalk.yellow('初始化完成 \n 已自动追加dev打包文件到build/*.json')) });
}

```
tasks/default.js
```js
const gulp = require('gulp');

gulp.task('default', gulp.series('create'));

```

tasks/create.js
```js
const gulp = require('gulp');
const path = require('path');
const chalk = require('chalk');
const fs = require('fs');
const { exec } = require('child_process');
const _template = require('lodash/template');

const baseTemplatePath = path.resolve(__dirname, '../../template/base');
const pluginNamePlaceholder = '<%= pluginName %>';
const escapedPluginNamePlaceholder = '\\<%=\\ pluginName\\ %\\>';
const pluginTitlePlaceholder = '<%= pluginTitle %>';
const escapedPluginTitlePlaceholder = '\\<%=\\ pluginTitle\\ %\\>';

// 项目模板文件拷贝
gulp.task('create:controller', function(callback) {
  console.log(chalk.green('-> task: create:controller \n'));
  const { pluginName, outputPath } = gulp.customParams;

  const controllerFile = fs.readFileSync(`${baseTemplatePath}/app/IndexController.js`);
  const targetControllerPath = `${outputPath}/app/controllers/${pluginName}`;
  const file = _template(controllerFile)({
    pluginName: pluginName
  });
  exec(`mkdir -p ${targetControllerPath} && cp ${baseTemplatePath}/app/mock.js ${targetControllerPath}/mock.js `, function(err, stdout, stderr) {
    fs.writeFileSync(`${targetControllerPath}/IndexController.js`, file);
    callback();
  });
})

gulp.task('create:router', function(callback) {
  console.log(chalk.green('-> task: create:router \n'));
  const { pluginName, outputPath } = gulp.customParams;

  const routerFile = fs.readFileSync(`${baseTemplatePath}/app/router.js`, 'utf8');
  const targetRouterPath = `${outputPath}/app/routers`;

  const file = routerFile.replace(new RegExp(pluginNamePlaceholder, 'g'), pluginName);
  exec(`mkdir -p ${targetRouterPath}`, function(err, stdout, stderr) {
    fs.writeFileSync(`${targetRouterPath}/${pluginName}.js`, file);
    callback();
  })
});

gulp.task('create:view', function(callback) {
  console.log(chalk.green('-> task: create:view \n'));
  const { pluginName, pluginTitle, outputPath } = gulp.customParams;

  const routerFile = fs.readFileSync(`${baseTemplatePath}/app/index.html`, 'utf8');
  const targetRouterPath = `${outputPath}/app/views`;

  const file = routerFile.replace(new RegExp(pluginNamePlaceholder, 'g'), pluginName).replace(new RegExp(pluginTitlePlaceholder, 'g'), pluginTitle);

  exec(`mkdir -p ${targetRouterPath}/${pluginName}`, function(err, stdout, stderr) {
    fs.writeFileSync(`${targetRouterPath}/${pluginName}/index.html`, file);
    callback();
  });

});

gulp.task('create:client folder', function(callback) {
  console.log(chalk.green('-> task: create:client folder \n'));
  const { pluginName, pluginTitle, outputPath } = gulp.customParams;

  const targetPluginClientPath = `${outputPath}/client/pages/${pluginName}`;
  exec(`mkdir -p ${targetPluginClientPath} && cp -r ${baseTemplatePath}/client/test/* ${targetPluginClientPath}`, function(err, stdout, stderr) {
    if (err) {
      console.error(err);
    }
    // 扫描插件下所有包含<%= pluginName %>, <%= pluginTitle %>字样的文件并替换为插件名称
    // 注意-i 后的''为参数： https://stackoverflow.com/questions/6889360/how-to-substitute-without-creating-intermediate-file-in-sed/6889366
    exec(`sed -i '' 's/${pluginNamePlaceholder}/${pluginName}/g' \`grep -lr ${escapedPluginNamePlaceholder} ${targetPluginClientPath}\``, function(err, stdout, stderr){
      if (err) {
        console.error(err);
      }

      exec(`sed -i '' 's/${pluginTitlePlaceholder}/${pluginTitle}/g' \`grep -lr ${escapedPluginTitlePlaceholder} ${targetPluginClientPath}\``, function(err, stdout, stderr){
        if (err) {
          console.error(err);
        }
        callback();
      })
    });
  })
});

gulp.task('create', gulp.parallel('create:controller', 'create:router', 'create:view', 'create:client folder'));

```
这里注册的是create的task，该task包含一系列并行化的create:xxx task。

以`create:client folder`为例，该task实现的是复制模板目录下的整个client目录，并cp到指定pluginName下的目录，然后通过`sed`命令实现对所有的包含`<%= pluginName %>`占位符的文件进行替换。

使用到的是fs模块对文件的操作以及child_process模块执行shell脚本命令，主要通过这两种方式进行文件的复制、内容替换、文件读写等


##### 4. package.json添加调试npm script
```js
"scripts": {
    "dev": "NODE_ENV=development node bin/index.js",
    "dev:new-plugin": "npm run dev new-plugin"
  },
```

##### 5. 发包
```sh
npm publish
```

##### 6. 在上层应用中添加npm script以及dev dependency依赖
```js
"scripts": {
   "scripts": "utils",
   "scripts:new": "utils new-plugin"
}
"devDependencies": {
   "utils": "0.0.1",
}
```
注意此处的npm script是可以直接使用`utils`命令的，在sh环境下需要使用`npx utils`。

#### 总结
本文从最简需求角度出发分析一个最简单的cli工具如何编写，当然很多工具比如`commander`也可以选择不用，通过node api来解析各种参数等方式实现。当然这个并非重点，重点是分析、抽离方式的思考的过程与实现的几个关键点。