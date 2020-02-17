# Commit提交规范

> CHANGELOG
>
> 2020/01/17	文档建立



## Commit Message Conventions

目前业界广泛接纳的是[Angular.js](https://github.com/angular/angular.js/blob/master/DEVELOPERS.md#commits)在Github上的提交规范。

业界广泛采用的是基于Angular.js在github上的提交规范[]()

```
<type>(<scope>): <subject>

<body>

<footer>
```

### type

`feat` 增加新特性

`fix` 修复bug

`docs` 文档改动

`style` 不影响代码实际意义的改动（空白字符、缩进格式，缺失的分号等等）

`refactor` 既不修复bug也不增加新特性的代码改动

`perf` 优化代码性能的改动

`test` 增加/修改测试点

`chore` build程序、辅助工具或库的变动

### scope

说明本次commit影响的范围

### subject

综述本次commit的改动

- 动词使用第一人称，现在式，e. g. Use "change" not "changes" nor changed"
- 首字母不用大写
- 末尾不加句号，冒号

### body

改动的body包含改动的原因，并与之前的行为进行比较

### footer

- 本次提交出现`BREAK CHANGE`（发生API不兼容情况）时，使用BREAK CHANGE标注前后的变化

- 如果当前commit针对某个*issue*,可以在footer部分指定关闭该issue



## References

Angular.js github: https://github.com/angular/angular.js/blob/master/DEVELOPERS.md#commits
