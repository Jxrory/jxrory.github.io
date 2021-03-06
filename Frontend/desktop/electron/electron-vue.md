# electron 中使用 vue

## 搭建 vue 环境

需要先安装 vue 命令行, 如果已经安装自行跳过.

```bash
npm install -g @vue/cli
```

**创建项目**:

```bash
# 下方 my-project 为项目名，可自己定义
vue create my-project
```

## 配置 Electron

```bash
cd my-project

vue add electron-builder
```

## 启动

```bash
npm run electron:serve
```

## 构建

**构建命令配置**:

```js
    "electron:build": "vue-cli-service electron:build",
    "electron:build-win": "vue-cli-service electron:build --win --x64",
    "electron:build-mac": "vue-cli-service electron:build --mac",
    "electron:build-linux": "vue-cli-service electron:build --linux",
```

## 参考

[最简洁 Vue+Electron 项目搭建教程](https://zhuanlan.zhihu.com/p/335225253)
[electron+vue 开发项目总结](https://juejin.cn/post/7012894751116492814)
