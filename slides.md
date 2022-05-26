---
theme: seriph
background: https://source.unsplash.com/collection/94734566/1920x1080
class: text-center
highlighter: shiki
lineNumbers: false
info: |
  ## 民主生活会
  大家一起来发包。[查看更多](https://wiki.qianxin-inc.cn/pages/viewpage.action?pageId=525117683)
drawings:
  persist: false
title: 民主生活会
titleTemplate: '%s - 天兵'
---

# Monorepos 介绍
BBFE-江城 [天兵]

<div class="pt-12">
  <span @click="$slidev.nav.next" class="px-2 py-1 rounded cursor-pointer" hover="bg-white bg-opacity-10">
    开始 <carbon:arrow-right class="inline"/>
  </span>
</div>

<!--
找点故事
-->

---

# npm包的关键点

- package.json配置
- 代码存储
- 版本管理
- npm源

<br>
<br>

接下来我们一起去实地操作一下……

<!--
邀请大家补充，然后自己操作一遍
-->

<style>
h1 {
  background-color: #2B90B6;
  background-image: linear-gradient(45deg, #4EC5D4 10%, #146b8c 20%);
  background-size: 100%;
  -webkit-background-clip: text;
  -moz-background-clip: text;
  -webkit-text-fill-color: transparent;
  -moz-text-fill-color: transparent;
}
</style>

---
layout: image-right
image: https://images.unsplash.com/photo-1652533875528-acd81de06ba7?ixlib=rb-1.2.1&raw_url=true&q=60&fm=jpg&crop=entropy&cs=tinysrgb&ixid=MnwxMjA3fDB8MHxwaG90by1yZWxhdGVkfDJ8fHxlbnwwfHx8fA%3D%3D&auto=format&fit=crop&w=500
---

# npm包实操

1. 去github创建一个存储源码的空仓库
2. 把空仓库拉下来
3. 开始初始化我们的npm包
```bash {all|1-2|3-4|5-6|7-9|10-11|12-13|14-15|all}
# 创建一个目录
mkdir npm-demo
# 编辑器打开
code npm-demo
# 初始化npm包配置
npm init
# 提交源码
git add .
git cia 'feat: init npm包'
# 确定版本
npm version patch
# 提交源码
git push && git push --tags
# 发布npm包到npm源
npm publish
```

---

# 大型npm仓库的烦恼(multirepos)

例如vue、babel、webpack等等，它们的生态越来越繁荣，能力越来越多，因此需要对功能进行拆分，单独发包，但是单独发包对于原来的开发方式会存在一些问题，比如：
* 代码不好复用 
* 本地调试不方便, 内部功能相互依赖，每次都要发包装包
* npm公共依赖无法复用，每个仓库都要install，占用很多本地空间，还会造成版本依赖不统一
```json
"@vue/cli-service@5.0.3":
  version "5.0.3"
  resolved "https://registry.npm.qianxin-inc.cn/@vue/cli-service/download/@vue/cli-service-5.0.3.tgz#878ae4045773fddff4f8d25edd1f8bd82dc1660d"
  integrity sha1-h4rkBFdz/d/0+NJe3R+L2C3BZg0=
  dependencies:
    "@babel/helper-compilation-targets" "^7.12.16"
    "@types/minimist" "^1.2.0"
    "@vue/cli-overlay" "^5.0.3"
    "@vue/cli-plugin-router" "^5.0.3"
    "@vue/cli-plugin-vuex" "^5.0.3"
    "@vue/cli-shared-utils" "^5.0.3"
    "@vue/component-compiler-utils" "^3.3.0"
    "@vue/vue-loader-v15" "npm:vue-loader@^15.9.7"
    "@vue/web-component-wrapper" "^1.3.0"
```

---
class: bg-white
---

# Monorepos思想

<div align="center">
<img src="https://static001.geekbang.org/infoq/d8/d86a0baaf0a1bc0d9f44201dacd7071f.png" width="500" />
</div>

---
layout: image-right
image: https://images.unsplash.com/photo-1653311918738-0c43e51fb962?crop=entropy&cs=tinysrgb&fm=jpg&ixlib=rb-1.2.1&q=80&raw_url=true&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=687
---

# 最佳实践 - lerna

轰隆隆！！！，lerna横空出世

Lerna 是一个管理工具，用于管理包含多个软件包（package）的 JavaScript 项目。目前Babel、Vue、 React、Angular、Ember、Meteor、Jest等都在用它。

主要提供的能力：
* 添加子模块
* 添加npm依赖
* 安装依赖
* 版本控制
* 模块发布

---
layout: center
class: text-center
---

# 一起现场操作一遍吧
大家一起来，come on~~~

---
layout: fact
---

# lerna实践

```bash {monaco}
# 安装lerna
yarn global add lerna
# 初始化为lerna项目
lerna init
# 新建包
lerna create <pkgname> <location>
# 添加npm依赖
lerna add <pkgname> [--scoped <scopeModule>]
# 发布包
lerna publish
```

[更多指令](http://www.febeacon.com/lerna-docs-zh-cn/routes/commands/)
