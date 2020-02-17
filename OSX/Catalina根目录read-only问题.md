# Catalina版本根目录read-only的问题

Mac升级到Catalina版本后，在根目录下执行写操作(如创建文件夹)会提示：

```shell
mkdir: /data: Read-only file system
```

这会导致一些限定目录的服务配置不可用(如Cat要求`/data/...`目录)



## 解决方案

1. 重启Mac，按住`command+R`进入恢复模式
2. 点击用户登录
3. 在顶部导航栏选择`Utilities->Terminal.app`
4. 输入指令`csrutil disable`，关闭SIP 
5. 点击左上角苹果的logo重启
6. 重启后在Terminal中输入`sudo mount -uw /`重新挂载根目录
7. 在根目录正常创建文件夹
8. 将其他目录的文件夹软连接到根目录文件夹`ln -s /Users/xxxx/test /test/`
9. 设置777或者其他读写权限
10. 重启并按`command+R`进入恢复模式
11. 在恢复模式的Terminal输入`csrutil enable`重新开启SIP
12. 重启

## 参考文章

https://stackoverflow.com/questions/58480473/how-to-solve-read-only-file-system-problem?r=SearchResults

https://www.v2ex.com/t/607330

http://www.au92.com/post/macos-catalina-readonly/

