# 使用说明
主要是两个配置文件，项目下的_config.yml 以及themes的_config.yml。

clone下来后进行:

```
npm install
```

然后进入themes进行

```
git clone maupassant
```

并将maupassant的配置文件覆盖。

```
hexo new [new blog name]
hexo g #创建public文件
hexo s #启动本地server调试
hexo g -d #创建并部署.若失败，要进行 npm install hexo-deployer-git --save
