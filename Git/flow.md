# git work flow

## git flow

Vincent Driessen 在2010年提出一种git的开发模型, 很快成为了最流行的git团队协作开发流程.

### git flow 分支描述

master

master分支是git flow模型的主分支, master分支的HEAD代表了可发布的产品状态, 每一个合并的commit都代表了一个可发布的版本

develop

develop分支是开发分支, 同样也是一个长期存在的分支. develop分支的HEAD代表了下次发布的一个最新特性开发改动

feature

feature分支从develop分支开出, 新特性开发完成后合并回到develop分支, 代表为下一次发布增加一个新的特性

release

release分支从develop分支开出, 测试, 修复bug完成后合并到develop和master分支. 当一个版本的开发达到一个相对稳定的状态, 从develop分支开出一个新的release分支.

hotfix

release分支从master分支开出, 问题修复完成后合并到develop和master分支. 当线上版本出现问题, 会紧急开出一个hotfix分支进行问题修复.

### git flow 流程描述

团队会维持2个长期的主要分支: master & develop.

新版本开发:
    开发人员从develop分支开出多个feature分支, 根据需求进行开发, 当特性开发完成后, 将feature分支合并到develop分支. 当下次版本发布所要求的新特性都开发完成后, 从develop分支开出一条release分支, 之后不会再有任何特性的改动, 只进行bug的修复. 在release分支上进行测试, bug修复, 当测试完成后, 将release分支合并到develop分支和master分支, 进行发布.

### git flow 存在问题

- 复杂度

## github flow

github flow是github所推荐的work flow, 在github上广泛应用于开源项目的协作开发

> GitHub flow is a lightweight, branch-based workflow that supports teams and projects where deployments are made regularly.

### github flow 分支描述

master

github flow只存在一条主要分支, master. 通过打上tag的方法标记特定的版本.

feature/fix

新特性开发/bug修复, 都是从master分支开出, 开发完成后合并回到master分支.

### github flow 流程描述

github flow工作的主要流程如下.

从master分支新建分支, 进行新特性的开发, 当开发完成后提交pull request(PR), 这时候所有人都可以看到并对代码做出评论, 开发者可以根据反馈继续进行开发, 新的commit也会反映在PR上. 当一次PR经过了code review, 可以将当前PR的最新提交部署到一个临时环境中进行验证, 一般会返回所部署临时环境的URL地址.

## gitlab flow

<https://docs.gitlab.com/ee/topics/gitlab_flow.html>

### gitlab flow 分支描述
