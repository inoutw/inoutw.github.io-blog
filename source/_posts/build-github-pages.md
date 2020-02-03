---
title: Hexo搭建Github Pages
---
之前按照github pages官方文档搭建了一个简易博客系统，发现没有可用的目录或者导航。偶然发现了一个博客框架，[hexo](https://hexo.io/docs/)，尝试了一下，还不错。

## Quick Start  
按照文档安装依赖，init了一个初始系统后。运行hexo server，就可以在本地开启博客系统

## 问题

### 配置next主题  
默认主题是landscape，我本人比较喜欢[next主题](https://theme-next.org/docs/getting-started/installation)  
根据提示，下载next主题后在本地会看到本地thems下多了一个文件夹 next

### CI

刚开始按照文档配置了travis CI，推送代码到远程master后自动生成gh-pages分支（最终的部署代码），然后需要在仓库settings里修改github pages的source分支为gh-pages，但是无法修改，[参考](ttps://stackoverflow.com/questions/39978856/unable-to-change-source-branch-in-github-pages)。  

解决办法：运用本地部署，然后推送部署代码到远程master[参考](https://hexo.io/docs/one-command-deployment)  

相应的_config.yml文件的改动

``` bash
deploy:
  type: git
  repo: https://github.com/xxx/xxx.github.io
```
然后运行

``` bash
$ npm install hexo-deployer-git --save  
$ hexo clean && hexo g && hexo deploy.

```

现在就可以看到你的站点: https://xxx.github.io 啦



More info: [Writing](https://hexo.io/docs/writing.html)

### Run server

``` bash
$ hexo server
```

More info: [Server](https://hexo.io/docs/server.html)

### Generate static files

``` bash
$ hexo generate
```

More info: [Generating](https://hexo.io/docs/generating.html)

### Deploy to remote sites

``` bash
$ hexo deploy
```

More info: [Deployment](https://hexo.io/docs/one-command-deployment.html)
