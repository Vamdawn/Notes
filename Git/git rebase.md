# git rebase 用法解读

变基

## 命令参数

```shell
git rebase [-i | --interactive] [<options>] [--exec <cmd>] [--onto <newbase> | --keep-base] [<upstream> [<branch>]]

git rebase [-i | --interactive] [<options>] [--exec <cmd>] [--onto <newbase>] --root [<branch>]

git rebase (--continue | --skip | --abort | --quit | --edit-todo | --show-current-patch)
```

## 执行效果

### 不简单的描述

针对上述第一种指令形式

- 若已指定`<branch>`，则会先切换到指定的`<branch>`，再进行rebase操作
- 若未指定`<upstream>`，则会以配置中的`branch.<name>.remote`和`branch.<name>.merge`作为`<upstream>`
- 存在于当前分支，但不存在于`<upstream>`的所有commits会被存储到一个暂存区域
- 当前分支会被reset到`<upstream>`，如果提供了`--onto <newbase>`则会被reset到`<newbase>`，相当于命令`git reset --hard <upstream>`
- 位于暂存区域的commits会按顺序重新提交，注意此时会有不同的commit id(若有冲突也需要解冲突)


## 简单应用

### 变基

```shell
# 假设:
# A - B - C - D - E branch1
#      \
#        F - G - H branch2
git rebase branch1 branch2
# 变基后
# A - B - C - D - E branch1
#                  \
#                   F - G - H branch2
```
