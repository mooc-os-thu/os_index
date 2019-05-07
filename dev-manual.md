# commit msg 规范
参考 [http://karma-runner.github.io/0.10/dev/git-commit-msg.html](http://karma-runner.github.io/0.10/dev/git-commit-msg.html)

# 图片规范
尽量少在仓库里面放图，避免增大项目体积。

如果要放方格状示意图，参考以下用字符形式呈现的图，除了手画不知道有什么好方法，有推荐的生成插件请务必提issue告知
```
/* Virtual memory map:                                          Permissions
 *                                                              kernel/user
 *
 *     4G ------------------> +---------------------------------+
 *                            |                                 |
 *                            |         Empty Memory (*)        |
 *                            |                                 |
 *                            +---------------------------------+ 0xFB000000
 *                            |   Cur. Page Table (Kern, RW)    | RW/-- PTSIZE
 *     VPT -----------------> +---------------------------------+ 0xFAC00000
 *                            |        Invalid Memory (*)       | --/--
 *     KERNTOP -------------> +---------------------------------+ 0xF8000000
 *                            |                                 |
 *                            |    Remapped Physical Memory     | RW/-- KMEMSIZE
 *                            |                                 |
 *     KERNBASE ------------> +---------------------------------+ 0xC0000000
 *                            |                                 |
 *                            |                                 |
 *                            |                                 |
 *                            ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
 */
//
// +--------10------+-------10-------+---------12----------+
// | Page Directory |   Page Table   | Offset within Page  |
// |      Index     |     Index      |                     |
// +----------------+----------------+---------------------+
//  \--- PDX(la) --/ \--- PTX(la) --/ \---- PGOFF(la) ----/
//  \----------- PPN(la) -----------/
//
```

# 分支规范
分支请带上目标后缀，比如我要为lab2增加注释

> git checkout -b verbose-dev-lab2

# 如何同步fork过来的仓库

输入 git remove -v，按下回车键，你将会看到你的 fork 当前配置的远程仓库：
```
$ git remote -v
origin	git@github.com:mooc-os-thu/ucore_os_lab.git (fetch)
origin	git@github.com:mooc-os-thu/ucore_os_lab.git (push)
```

添加原始仓库地址
```
$ git remote add upstream git@github.com:chyyuu/ucore_os_lab.git
$ git remote -v
origin	git@github.com:mooc-os-thu/ucore_os_lab.git (fetch)
origin	git@github.com:mooc-os-thu/ucore_os_lab.git (push)
upstream	git@github.com:chyyuu/ucore_os_lab.git (fetch)
upstream	git@github.com:chyyuu/ucore_os_lab.git (push)
```

切换到主分支，同步代码到本地，从本地同步到我们的仓库
```
$ git checkout master
$ git merge upstream/master
$ git push
```

