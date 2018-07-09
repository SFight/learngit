# learngit
主要记录下git的一些学习记录

# 2018-07-04 向github提交库的时候的两个库的合并
  今天在提交GitHub的时候，由于测试工程和Framework库的工程不属于一个git库，但是又不想在GitHub开两个工程，所以才有了合并库的想法。
  百度了下，发现这种操作原来还是有的，不知道对不对，但是至少能解决问题，可能比较野路子。
  * 1、有两个库A和B，将B库内容合并到A库中；
  * 2、在A库中添加remote，例如：git remote add 仓库名称 仓库地址;
  * 3、在A库中进行fetch远端，例如：git fetch 添加的远端仓库名;
  * 4、在A库中创建分支，并将新添加的remote checkout下来，例如：git checkout -b 分支名称 仓库名称/仓库对应的分支名称
  * 5、此时已经在新创建的分支中了，我创建的是local分支，然后将local分支与master分支合并，git merge master（注意：此处会报错fatal: refusing to merge unrelated histories，因为这两个库并不在统一的库中记录，所以需要加个参数--allow-unrelated-histroies）
  * 6、此时local分支为要合并的A库和B库的所有内容，此时再切换为A库的master，然后merge local就好了。
  #### 跟朋友沟通，了解到了更简单的操作。。。看来是我想太多啊。。git merge 远端库/分支名 直接操作就好。
  
# 2018-07-05 向github提交的时候卡在Writing objects: 
  今天在向github提交的时候，由于项目比较大，导致开在了Writing objects:  57% (154/270)，一直不知道是什么原因，以为是网速导致，因为后边提交的时候速度直接降到了几kb/s，看起来并无什么问题，然而实际上是由于http缓存导致的。可以全局设置下，命令如下：
  ```git
  git config --global http.postBuffer 524288000
  ```
# 2018-08-06 因为修改了submodule的内容，导致主工程出现submodule的status中提示了submodule内有内容修改的提示，需要提交
  今天在修改自己写的一个阅读器代码的时候，对submodule修改了测试代码，后边又修改回去了，但是在主工程中出现了提示，需要提交，后来发现，实际上是对submodule的使用不太对，应该是纯readonly的引用才对。
  通过修改.gitmodules，对相应的submodule添加ignore字段，字段的内容可以有三个，如下：
  untracked ：忽略 在子模块B(也就是projectB目录)新添加的，未受版本控制内容
  dirty ： 忽略对projectB目录下受版本控制的内容进行了修改
  all ： 同时忽略untracked和dirty
  我这里直接修改成all，因为是只读引用，忽略主工程内的所有需要提交的东西。
