## Git 使用规范

饿了么大前端团队使用git作为协作工具，使用Github作为代码仓库。这份文档包含了一些git命令，但这是一份团队的git使用规范，不是一份git的使用说明。如需了解git如何使用，请移步[这里](https://git-scm.com/)，或者[这里](https://www.atlassian.com/git/tutorials/)。

### 开启二次验证
为避免被管理员剔除出github上的开发团队，请务必开启github账号的二次验证。开启位置 `Settings` => `Security` => `Two-factor authentication`

### fork工作仓库
每次开始一个项目前，在clone主仓库代码后，请务必fork该项目，然后在你的本地仓库添加你fork后的仓库地址：

```
$git remote add yourremote git@github.com:youraccount/projectname.git
```

此时

```
$git remote -v
origin	git@github.com:eleme/projectname.git (fetch)
origin	git@github.com:eleme/projectname.git (push)
yourremote	git@github.com:youraccount/projectname.git (fetch)
yourremote	git@github.com:youraccount/projectname.git (push)
```

每次提交代码，请先将代码提交到你的远程分支：

```
$git push yourremote currentbranch:remotebranch
```

### 在最新的代码上开始工作

每次开始工作前，请确保你的代码是基于合并目标分支（一般是发布分支主分支）的最新代码，因此推荐从该主仓库该分支拉取最新代码新建一个分支：

```
$git fetch origin master:newbranch
```

### Commit
我们希望您*Commit Early And Often*，因为这样会记录您在开发过程中的主要变动，在您的开发遇到问题时很容易回退到某个commit。这样，在一次开发完毕后会产生较多commit，这些commit对于要合并的目标分支来讲一般是不必要的。所以，在开发完毕后查看一下commit信息

```
$git log
```

然后将多余的commit信息合并进一条（最多2~3条）主要的commit里，例如，目前分支共有有多个新的commit，那么你可以：

```
$git rebase -i origin/master
```
更多介绍可参考[这篇文章](https://robots.thoughtbot.com/git-interactive-rebase-squash-amend-rewriting-history)
### Commit messages
commit信息可以让其他开发者无需阅读代码便快速了解你做了哪些变动。commit信息的主题应该简洁明了，我们希望它包含如下信息：

```
action + target + (position)
```
总结一句话就是：你在哪对谁都干了什么？
例如：

```
Refactor subsystem X for readability
Update getting started documentation
Remove deprecated methods in page x
```
下面是一些不好的示例：

```
// 在哪个模块和页面改了什么？
改！
诊断：缺少target和position。

// 什么bug？在哪出现的？
Fix a bug
诊断：缺少对target必要地描述和position

// 做了什么改动还是新建了这个页面？
积分商城
诊断：缺少action以及target不够具体
```

### Pull Request
在发[Pull request](https://help.github.com/articles/using-pull-requests/)之前，要再一次从您希望合并的目标分支拉取最新代码，并且，为避免产生`merge`信息，请使用`--rebase`参数：

```
$git pull --rebase origin master
```

此时，如果其他人也改过同一部分代码，会产生冲突，在解决冲突后：

```
$git add .
$git commit
```
此时可以将代码发到自己远程分支，然后向要合并的分支发一个`Pull request`，打上合适的`Label`，并且`@`2~3相关人员来`review`你的代码。

### Label
为`Pull request`标注合适的`Label`，可以在让合作者清楚这个pr的进度和状态。例如，在外卖平台组，我们采用这样的`Label`:

`developing`：pr依然在开发状态；
`need review`：开发完毕，希望合作者提出意见；
`testing`：非常重要，打上这个表情，当使用`make testing`发布到测试环境进行测试时，所以带该标签的pr都会合并在一起进行测试，共用测试环境。
`test passed`：测试已经通过。
`want merge`：这个标签意味着在「最近的发布计划」里（显然也是测试通过的），负责发布的同学在发布前要看一下发布计划以及pr列表，检查还有没有打了这个标签但是没合掉的。没在发布计划里却打了这个标签要再找开发者确认一下（例如一些我们自己的改进）。

项目的负责者要维护好项目的`Label`，为开发者提供便利。

### Merge
主分支发布的项目，Pull request合并前需要经过`code review`以及相关测试人员测试。在这个阶段此pr可打上`need review`，只有打上`want merge`的pr可以合并进主分支等待发布。

尽量避免自己合并代码。在pr收到两个或两个以上:thumbsup:或『可以合并』评论后可以自己合并。

### 项目交接
如果在一个项目需要交接或者本人需要离职前，还有未完成的代码，请务必将未完成的代码提交到主仓库的一个临时分支，然后发一个到master分支的pull request并且打上`developing`标签，写明必要地描述并at相关交接人员。

##### *Reference*
* [Commit Often, Perfect Later, Publish Once: Git Best Practices](http://sethrobertson.github.io/GitBestPractices/)
* [A Note About Git Commit Messages](http://tbaggery.com/2008/04/19/a-note-about-git-commit-messages.html)
* [How to Write a Git Commit Message](http://chris.beams.io/posts/git-commit/)
* [Git Commit Messages : 50/72 Formatting](http://stackoverflow.com/questions/2290016/git-commit-messages-50-72-formatting)
* [5 Useful Tips For A Better Commit Message](https://robots.thoughtbot.com/5-useful-tips-for-a-better-commit-message)
* [Git Protocol](https://github.com/thoughtbot/guides/tree/master/protocol/git)
* [Git Interactive Rebase, Squash, Amend and Other Ways of Rewriting History](https://robots.thoughtbot.com/git-interactive-rebase-squash-amend-rewriting-history)