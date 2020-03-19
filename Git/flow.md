# git 开发模型

## git flow

### git flow 分支描述

master

git flow模型的master分支表现为产品发布的状态, 每一个commit都代表一个可以发布的版本

develop

开发分支包含了当前正在开发的新特性

feature

从develop分支开出feature分支, 开发完成后, 合进develop分支

release

当一次新特性开发完成后, 从develop分支开出一个release分支, 部署后在其上进行测试, 此时不再添加新特性, 只进行bug的修复

hotfix

当线上版本出现问题, 从master分支开出hotfix分支, 修复完成后, 同时合进develop和master分支

### git flow 流程描述

团队维持2个主要分支: master & develop.

每当有新需求, 有新特性需要开发, 从develop分支开出feature分支, 由开发人员在feature分支进行开发, 对于本次发布要发布的新特性, feature分支需要在规定期限内开发完成, 合并进develop分支.

当本次所有新特性开发完成, 合并进develop分支后, 从develop分支开出release分支, 此后不再向release分支做任何新特性的添加或修改, 只在relase分支上进行bug的修复, bug修复完同样要同步到develop分支. 当测试没问题, release分支稳定下来, 即准备将release分支合并进master分支, 进行一次新版本的发布.

当线上出现问题时, 要从master分支紧急开出一个hotfix分支, 进行修复, 测试, 完成后合并到master和develop分支.

### git flow 存在问题

WIP

## github flow

### github flow 分支描述

master

只存在1条主要分支, 即master, 以tag的形式代表版本发布

feature/fix

无论是新特性还是bug修复, 都直接从master分支开出, 然后合并回master分支

### github flow 流程描述



## gitlab flow

<https://docs.gitlab.com/ee/topics/gitlab_flow.html>
