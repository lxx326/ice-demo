## Antd Design & icejs scaffold

## 使用

```bash
# 安装依赖
$ npm install

# 启动服务
$ npm start  # visit http://localhost:3333
```

[More docs](https://ice.work/docs/guide/about).

## 目录

```md
├── build/ # 构建产物
├── mock/ # 本地模拟数据
│ ├── index.[j,t]s
├── public/
│ ├── index.html # 应用入口 HTML
│ └── favicon.png # Favicon
├── src/ # 源码路径
│ ├── components/ # 自定义业务组件
│ │ └── Guide/
│ │ ├── index.[j,t]sx
│ │ ├── index.module.scss
│ ├── layouts/ # 布局组件
│ │ └── BasicLayout/
│ │ ├── index.[j,t]sx
│ │ └── index.module.scss
│ ├── pages/ # 页面
│ │ └── Home/ # home 页面，约定路由转成小写
│ │ ├── components/ # 页面级自定义业务组件
│ │ ├── models.[j,t]sx # 页面级数据状态
│ │ ├── index.[j,t]sx # 页面入口
│ │ └── index.module.scss # 页面样式文件
│ ├── configs/ # [可选] 配置文件
│ │ └── menu.[j,t]s # [可选] 菜单配置
│ ├── models/ # [可选] 应用级数据状态
│ │ └── user.[j,t]s
│ ├── utils/ # [可选] 工具库
│ ├── global.scss # 全局样式
│ ├── routes.[j,t]s # 路由配置
│ └── app.[j,t]s[x] # 应用入口脚本
├── build.json # 工程配置
├── README.md
├── package.json
├── .editorconfig
├── .eslintignore
├── .eslintrc.[j,t]s
├── .gitignore
├── .stylelintignore
├── .stylelintrc.[j,t]s
├── .gitignore
└── [j,t]sconfig.json
```

## umi->ice

没有使用 dva 的情况下迁移 0 成本：

1. [样式]修改.less 文件为.module.less，并修改引入；
2. [去 umi]去除页面从 umi 导入的方法；
3. [资源模块]vite 模式下 页面不要有 require 的模块和资源，换成 import 的方式；
4. [注意].ts,.js 没有配置 loader，如果返回 JSX.Element 请换成 jsx,tsx;
5. [model]删除页面级别的 model.ts 文件，统一在 src/models 下维护

## 遇到的问题

1. 飞冰默认下载的模板会有警告 在 build.config.ts 配置 esbuild-logOverride 内容
2. 添加 gitHooks->commit-msg 及 verify-commit-msg.js 之后 commit 并不会校验生效，还需要下载 yorkie 依赖
3. 部署页面使用 pages-> /docs 方式，部署页面遇到的问题 https://github.community/t/pages-deploy-wedged-incorrect-request-failed-due-to-in-progress-deployment/234793
   部署之后静态文件 404， 需要在 build.config.ts 中添加 publicPath
4. 使用 fastmock 生成的接口对接，在 app.tsx 添加 request->baseURL 即可， 遇到的接口超时为 fastmock 问题
