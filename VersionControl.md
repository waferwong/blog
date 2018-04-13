
# Git
[Git - Book](https://git-scm.com/book/zh/v2)
[Git教程 - 廖雪峰的官方网站](http://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000/)

不输入密码
[ssh-key 与 git账户配置以及多账户配置 - dubaokun - 博客园](http://www.cnblogs.com/dubaokun/p/3550870.html)
[git如何push时不输入密码? - 知乎](https://www.zhihu.com/question/31836445)
[Caching your GitHub password in Git - User Documentation](https://help.github.com/articles/caching-your-github-password-in-git/)

[git inside --simplified --part '1'](https://zhuanlan.zhihu.com/p/27474934)
[git inside --simplified --part '2'](https://zhuanlan.zhihu.com/p/27556941)

[Git如何使用GUI（图形化）Diff工具查看两个分支或是标签的Diff - 李鼎的博客 | Jerry Lee's Blog](http://oldratlee.com/post/2012-10-25/git-check-diff-between-tag-or-branch-using-gui-diff)
[version control - Reset or revert a specific file to a specific revision using Git? - Stack Overflow](https://stackoverflow.com/questions/215718/reset-or-revert-a-specific-file-to-a-specific-revision-using-git)

## gitlab


### ci
[如何为持续集成平台选型？](https://mp.weixin.qq.com/s/ND_yL3AqFm_5Dl1whcHgzg)
jenkins
[前端开发如何让持续集成/持续部署(CI/CD)跑起来 | 安·记](http://annn.me/frontend-ci-cd/)
[Jenkins Gitlab持续集成打包平台搭建 | SkySeraph](http://skyseraph.com/2016/07/18/Tools/Jenkins%20Gitlab%E6%8C%81%E7%BB%AD%E9%9B%86%E6%88%90%E6%89%93%E5%8C%85%E5%B9%B3%E5%8F%B0%E6%90%AD%E5%BB%BA/)

[Configuration of your jobs with .gitlab-ci.yml - GitLab Documentation](https://docs.gitlab.com/ce/ci/yaml/README.html)
[Gitlab CI yaml官方配置文件翻译 - 麦奇 - SegmentFault](https://segmentfault.com/a/1190000010442764)
[gitlab-ci配置详解(一) - 前端学习 - SegmentFault](https://segmentfault.com/a/1190000011881435)


[用 GitLab CI 进行持续集成 - scarlex - SegmentFault](https://segmentfault.com/a/1190000006120164)
[GitLab-CI与GitLab-Runner - 简书](https://www.jianshu.com/p/2b43151fb92e)
[GitLab-CI 从安装到差点放弃 - 前沿开发团队 - SegmentFault](https://segmentfault.com/a/1190000007180257)
[Docker 及 GitLab CI 在前端工作流上的实践分享（二） - 前沿开发团队 - SegmentFault](https://segmentfault.com/a/1190000011553991)
[Gitlab CI Multi Runner搭建CI持续集成环境 - CSDN博客](http://blog.csdn.net/lusyoe/article/details/52714121)
[基于Gitlab CI搭建持续集成环境 - 简书](https://www.jianshu.com/p/705428ca1410)
[[后端]gitlab之gitlab-ci自动部署 - 简书](https://www.jianshu.com/p/df433633816b)
[How to use GitLab CI for Vue.js | GitLab](https://about.gitlab.com/2017/09/12/vuejs-app-gitlab/)

#### 安装
[清华大学开源软件镜像站 | Tsinghua Open Source Mirror](https://mirrors.tuna.tsinghua.edu.cn/help/gitlab-ci-multi-runner/)

#### 注册
要接着向gitlab-CI注册这个runner，不然gitlab-CI在push事件到来的时候怎么知道要调用谁呢？这里也可以发现和webhook方式的区别，webhook方式是我们主动配置了一个连接给gitlab；gitlab-runner只要注册一下就好了。

$ gitlab-ci-multi-runner register
#引导会让你输入gitlab的url，输入自己的url，例如http://gitlab.example.com/
#引导会让你输入token，去相应的项目下找到token，例如ase12c235qazd32
#引导会让你输入tag，一个项目可能有多个runner，是根据tag来区别runner的，输入若干个就好了，比如web,hook,deploy
#引导会让你输入executor，这个是要用什么方式来执行脚本，图方便输入shell就好了。

#### .gitlab-ci.yml

su gitlab-runner


# SVN
