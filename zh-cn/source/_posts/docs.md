---
title: EggBorn.js开发指南
date: 2017-10-17 18:18:14
tags: 文档
---

## EggBorn.js是什么
EggBorn.js是采用Javascript进行全栈开发的最佳实践。EggBorn.js不重复造轮子，而是采用业界最新的开源技术，进行全栈开发的最佳组合。前端采用Vue.js + Framework7 / Vue Router + Webpack，后端采用Koa.js + Egg.js，数据库采用mysql。EggBorn时刻跟踪开源技术的最新成果，并持续优化，使整个框架时刻保持最佳状态。

## EggBorn.js重点解决什么问题：业务模块化
Javascript技术的蓬勃发展，为前后端开发带来了更顺畅的体验，显著提升了开发效率。但仍有网友质疑Javascript能否胜任大型Web应用的开发。大型Web应用的特点是随着业务的增长，需要开发大量的页面组件。面对这种场景，一般有两种解决方案：

``` bash
采用单页面的构建方式，缺点是产生的部署包很大。
采用页面异步加载方式，缺点是页面过于零散，需要频繁与后端交互。
```

> EggBorn.js实现了第三种解决方案：页面组件按业务需求归类，进行模块化，并且实现了模块的异步加载机制，从而弥合了前两种解决方案的缺点，完美满足大型Web应用业务持续增长的需求。

## EggBorn.js的技术特点
- 业务模块化：页面组件按模块组织
- 加载方式灵活：模块既可异步加载，也可同步加载
- 模块高度内聚：模块包括前端页面组件和后端业务逻辑
- 参数配置灵活：模块中的前后端可以单独进行参数配置
- 国际化：模块中的前后端均支持独立的国际化
- 模块隔离：模块的数据、逻辑、路由、配置等元素均进行了隔离处理，避免模块之间的变量污染与冲突
- 渐进式开发：由于模块的高度内聚，可以将业务以模块的形式沉淀，在多个项目中重复利用，也可贡献到GitHub开源平台。

> 有了EggBorn.js，从此可复用的不仅仅是组件，还有业务模块。

## 快速上手

### 安装EggBorn.js脚手架

``` bash
$ npm i -g egg-born
```

### 新建项目

``` bash
$ egg-born project_name
```

> EggBorn.js目前提供了4个脚手架，分别是
> - front-backend-mysql  -- 前后端全栈项目模板
> - front                -- 前端项目模板，后端可采用其他方案
> - module               -- 全栈模块模板
> - module-front         -- 前端模块模板

### 配置mysql连接参数

如果采用了“front-backend-mysql”模板，请配置mysql连接参数（空数据库即可）。

``` javascript
# src/backend/config/config.default.js

  // mysql
  config.mysql = {
    clients: {
      // donot change the name  
      __ebdb: {
        host: '127.0.0.1',
        port: '3306',
        user: 'zhennann',
        password: 'egg-born',
        database: 'egg-born',
      },
    },
  };

```

### 运行项目

``` bash
$ cd project_name
$ npm run dev:backend  -- 启动后端
$ npm run dev:front    -- 启动前端
```

## EggBorn.js架构图

### 系统架构
![](/zh-cn/images/EggBornJS.png)

### 项目文件结构
![](/zh-cn/images/structure.png)

### 模块文件结构
![](/zh-cn/images/privatemodule.png)
![](/zh-cn/images/publicmodule.png)

## 前端开发

### 启动文件
前端架构提供两种方案
``` bash
Vue.js + Vue Router
Vue.js + Framework7
```
在`main.js`文件中进行切换
``` javascript
// choose one

//   framework7
import main from './framework7/main.js';

//   vuerouter
// import main from './vuerouter/main.js';

// export
export default main;
```

### 配置文件
`config.js`文件中的参数配置可以覆盖模块的参数
``` javascript
export default{
  module: {
    'aa-hello': {
    },
  },
};
```

### 国际化
在`locale`目录添加国际化文件，可以覆盖模块的国际化语言
`zh-cn.js`文件中的语言定义示例如下
``` javascript
export default {
  mode: '模式',
};
```

## 后端开发

### 后端架构
后端架构基于Egg.js，完整支持Egg.js提供的所有功能与特性
> 更多信息，请参阅: [Egg.js](https://eggjs.org/)

### 配置文件
`config.default.js`文件中的参数配置可以覆盖模块的参数
``` javascript
module.exports = appInfo => {
  const config = {};

  // keys
  config.keys = appInfo.name + '_{{keys}}';

  // module config
  config.module = {
    'aa-hello': {
    },
  };

  // mysql
  config.mysql = {
    clients: {
      // donnot change the name
      __ebdb: {
        host: '127.0.0.1',
        port: '3306',
        user: 'zhennann',
        password: 'egg-born',
        database: 'egg-born',
      },
    },
  };

  return config;
};
```

### 国际化
在`locale`目录添加国际化文件，可以覆盖模块的国际化语言
`zh-cn.js`文件中的语言定义示例如下
``` javascript
export default {
};
```

## 模块开发



## 测试
## 部署
## GitHub贡献
> 有任何疑问，欢迎提交 [issue](https://github.com/zhennann/egg-born/issues)， 或者直接修改提交 [PR](https://github.com/zhennann/egg-born/pulls)！





