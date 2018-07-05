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
