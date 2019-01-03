# Git 工作流

所谓git 工作流，就是用git来做vcs时候的一套工作流程

广义上讲，由于一般无论自建还是托管中心库都会带一个管理平台，事实上现在也就是github、gitlab、bitbucket这么几个选择，所以祥细说起来，应当包括如何在这些平台上发起issue和discussion并resovle和close的过程

考虑到这些过程很有可能被外化到例如JIRA等这类专业平台上做的情况，太复杂，所以这里限制在讨论从中心库master到撰写完内容要贡献回中心库master这段历程

[git导读篇](git-tutorial)，提到了git flow，并且提到了主要的[参考资料](http://www.ruanyifeng.com/blog/2015/12/git-workflow.html)

考虑到这个问题重要到几乎都快被遗忘了（还是未被重视？），所以有必要特别的提一下其中几个要点

+ 除非不得已（比如被老板强制），或者是自己进行知识拓展，否则不碰[git flow](https://nvie.com/posts/a-successful-git-branching-model/)应该没损失
  - 看他那个图就总觉得这位仁兄想把git拉回到svn视角
  - 按说他成文的时间应当是晚于被广泛接受的[分布式管理方式](https://git-scm.com/book/en/v1/Distributed-Git-Distributed-Workflows#Dictator-and-Lieutenants-Workflow)
  - 友情推测应当是形成这个规则的年代，大型商业软件的发版规则，内部协作方式都还比较传统（好像里有也不充分）
+ [github flow](https://guides.github.com/introduction/flow/) 可以认为就是和 [gitlab flow](https://docs.gitlab.com/ce/university/training/gitlab_flow.html) 就是一个东西，gitlab flow细化了代码合并到master之后的发版策略（这一点阮老师文章三言两语说的很清楚），因此可以不考虑他们的区别，只需要理解相同部分的精髓就行了
+ github flow 的核心也就是所谓精髓了，还是在于pull request，明确这个环节在于代码合并到权威库的特定分支（通常就是主分支、发布分支、默认分支，就是master）之前，可以做一系列的控制代码质量的事情，主要就是code review，其次很多实践倾向这里要进行一轮回归测试

如果由于种种原因使用了gitlab CE，要注意它砍掉了显式的针对review强化设计的功能，需要正确设置每一个project版本库的权限和保护分支策略来达到基本的目的

* 为有责任作为gatekeeper的人在project设置maintainer之上的role
* 其他仅贡献code但不适合有决策权的人，只给developer以下的role
* 确认对project的portected branch的设置，至少对master设置了protected（这是缺省的）
  - 建议把Allow to push 改成no one，这样即便是maintainer角色的账户也不能脱离merge request来豁免
  - 但是由于没有approved限制，maintainer 做merge request 是可以自产自销的
  - 因此maintainer角色账户的同学应当主动show自己的代码给其他人来检查
    * 后面会考虑同样基于discussion来做一定的功能强化，但是maintainer是有权限close discussion的，所以靠这个达到完全约束不自律的maintainer不太现实，毕竟纪律只适合约束愿意遵守纪律的人

另外，如果有私库加入到这个流程里面，github flow的主要流程（可能，完全看个人喜好）会变成这样：

1. fork central repo to your own repository
1. git clone from your own repository
1. git checkout -b feature/balabala 
1. happy working on feature/balabala and push anything to your own repository at anytime
1. rebase your working branch and push -f to your own repository
1. create PR or MR from your own repository/feature/balabala to central repository/master

私库的好处就是可以不给代码贡献者任何写权限，然后它还可以有个远端库肆意地虐，而不用污染其他人的视界，否则他干过的坏事所有人真的都知道这件事他即便不介意，repository的owner可能还真会介意，总之它其实给了所有人最大的自由度

gitlab CE的Repository Mirror功能很是奇怪，所以想用私库，目前目测只能靠私库owner自己来[sync]() with central了

这应该是常用的git workflow的全部了

鉴于前审很可能流于形式，因此PR时候进行的回归测试很有可能才是保证质量的真正第一道闸口

gitlab在这个问题上处理的也不够开放，估计是自己想推自家的CI/CD工具，如果用它自身的pipeline功能，需要在工程代码中植入他的pipeline配置文件

现在在尝试[使用jenkins](https://www.google.com/search?q=Gitlab+Merge+Request+Builder+Plugin&rlz=1C1GCEA_enUS805US805&oq=Gitlab+Merge+Request+Builder+Plugin&aqs=chrome..69i57j69i60l2&sourceid=chrome&ie=UTF-8)来对project的repo做无侵入的检测，思路大概就是通过webhook去触发一段脚本或一个服务去调用 gitlab的 api来为特定的merge request创建一个discussion，待回归测试通过则关闭discussion，然后配合gitlab merge request里面"Only allow merge requests to be merged if all discussions are resolved"来达到控制merge要满足测试通过这个条件

总之，在gitlab上实施git工作流和部署流水线这个问题上，感觉用gitlab CE就是用了个残废版，如果使用了它，共勉，自律吧