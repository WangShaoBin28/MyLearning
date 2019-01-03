# 导读资料

给认为对 git 还需要再了解的同学准备的，本来试着自己写一篇，刚写了个开头，目测没10天半个月也写不完，所以先贴一个别人的，毕竟，人家不仅写完了，也肯定比我瞎攥的好

要说入门导读，首推阮老师

- [常用 Git 命令清单](http://www.ruanyifeng.com/blog/2015/12/git-cheat-sheet.html)
- [Git远程操作详解](http://www.ruanyifeng.com/blog/2014/06/git_remote.html)
- [Git 使用规范流程](http://www.ruanyifeng.com/blog/2015/08/git-use-process.html)

阮老师也把guide叫规范了，这是小事情，他缺两个东西：

* 安装，可能阮老师用linux，所以就没考虑这个问题
* 手把手教学的范例，这个真的很难推荐，要不看这个吧：[猴子学git](https://backlog.com/git-tutorial/cn/)

猴子那个分三部分，入门、高级、索引，其实是各自成体系的，入门篇注意都是按mac、win、命令行三种客户端来介绍的，建议使用命令行，这个教程好在有安装！阮老师都不讲安装！猴子讲了！说明什么？

另外提一句如果有选择，工作流**尽量不要用**git flow，相关请重点熟悉[文章](http://www.ruanyifeng.com/blog/2015/12/git-workflow.html)（又是阮老师） 中 github flow 及其变种 gitlab flow的持续发布方式

# 大纲范围

阮老师那一套东西，都是言简意赅，其实基本上也就差不多了，但是如果跟着猴子学，内容有点多，因此这里划定一些命令范围，至少就能生存了

- git init
- git clone
- git pull
- git push
- git checkout [branch]
- git checkout -b [new_branch]
- git add
- git commit
- git commit -a
- git status
- git remote -vv
- git remote add
- git remote show
- git branch -avv

大致应该就这些，看上面资料搞明白这些干嘛的基本上就能生存了，可能还需要git config，不过总觉得这个命令，看屏幕提示来足够了，如果觉得学有余力，搞懂

- git fetch
- git merge [branch]
- git cherry-pick [commit]
- git rebase -i [commit]

等等等等，就随意了可以，oh btw

为什么用命令行呢，因为可以利用命令行的优势，比如我懒得去弄其他用来同步我多个远端库（为什么要这样？我也不知道，这是我自己的需要）的工具，那就可以这样来：

```
git remote | xargs -i git push {} master
```

当然这是临时想的，只有master分支，其实全部分支也没什么，什么？保护分支，我自己私库好像不用搞这么复杂吧

# 其他

- gitlab要配置公钥进行ssh访问，方便git的remote操作，至少看[这个](https://docs.gitlab.com/ce/ssh/README.html#adding-a-ssh-key-to-your-gitlab-account)
- git 工作流，阮老师[那篇](http://www.ruanyifeng.com/blog/2015/12/git-workflow.html)真的很好了，按说佛头着粪的事一直是我想努力避的，但这个问题确实有必要额外做个[导读](git-workflow)

如果说这里想强调点什么，那就是git和svn真的完全不一样，git不是装一个小海龟然后同步代码这点事儿（svn真的就把大家对它的认识退化成这样了），它是可以实实在在的来帮忙管好代码的，这里还没有涉及更有意思的东西，因为仅仅是日常的使用方面，已经提供了很多变化和可能性

具体基于 git 再扩展阅读，可以考虑从这两方面入手：

+ git 底层存储[实现和接口](https://git-scm.com/book/zh/v2/Git-%E5%86%85%E9%83%A8%E5%8E%9F%E7%90%86-%E5%BA%95%E5%B1%82%E5%91%BD%E4%BB%A4%E5%92%8C%E9%AB%98%E5%B1%82%E5%91%BD%E4%BB%A4)，git就是一个文档数据库系统，是可以考虑用它来实现点的什么
+ 知识不联系毋宁死，所以git和红到发紫的bc（bitcoin or block-chain）从直觉上是不是有点像？[参考1](https://zhuanlan.zhihu.com/p/33927320)，[参考2](https://medium.com/@shemnon/is-a-git-repository-a-blockchain-35cb1cd2c491)，[参考3](https://stackoverflow.com/questions/46192377/why-is-git-not-considered-a-block-chain)，[参考4](https://www.google.com)
