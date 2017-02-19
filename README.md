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

并将主题的配置文件覆盖。
修改云标签文件(layout/\_widget/tag.jade)中的tagcloud改为：
```
{min_font: 15, max_font: 30, amount: 100, orderby: 'count',color: true, start_color: '#000',end_color: '#FF0000'}
```

最后将images目录下的图片放在七牛云上

```
hexo new [new blog name]
hexo g #创建public文件
hexo s #启动本地server调试
hexo g -d #创建并部署.若失败，要进行 npm install hexo-deployer-git --save
