# vuepress
## 基础了解
[快速搭建项目](https://www.vuepress.cn/guide/getting-started.html)
[目录结构](https://www.vuepress.cn/guide/directory-structure.html)
[默认主题配置使用](https://www.vuepress.cn/theme/default-theme-config.html)

## 遇见过的问题
打包发布到Github Pages上之后跳转页面404。
通过页面跳转路径上看，少了一节项目名称（没使用用户名.github.io的方式）,
[需要将config.js中加入](https://blog.csdn.net/qq_28584685/article/details/88017069)
`base:项目名称`