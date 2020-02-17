# zsh可能踩到的坑

## zsh模式匹配符 * 和 ? 可能引发的问题

 在zsh中，`*`和`?`将默认被默认用于进行文件名的匹配（当然时在不满足别的zsh特殊格式的使用条件下）。这样可能引发一些问题：

```shell
curl https://www.baidu.com/     # 正常输出
curl https://www.baidu.com/?    # zsh: no matches found: https://www.baidu.com/?
curl "https://www.baidu.com/"   # 正常输出
curl "https://www.baidu.com/?"  # 正常输出
```

这类情况在旧版Mac所带的shell中则不会出现，使用zsh的小伙伴需要注意，使用的参数是否会涉及zsh的模式匹配符，如果有可以考虑将其使用引号包裹起来

参考文章：http://zsh.sourceforge.net/Guide/zshguide05.html



