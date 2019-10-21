---
layout:     post
title:      git submodule and git subtree
subtitle:   git submodule and git subtree
date:       2019-10-16
author:     Stackjolin
header-img: img/post-bg-kuaidi.jpg
catalog: true
tags:
    - Git
---





# git submodule & git subtree

git submodule 和 git subtree 是 git 内嵌的 ‘包依赖’ 功能模块。git subtree没有出现之前，git submodule是Git官方推荐的子项目管理方案，在git 1.5.2版本之后。git subtree出现了，相同的，git subtree成了官方努力推荐的子模块管理方案



#### git submodule原理

------

主项目A保存子模块B的某次commit，用以表示使用主项目使用子项目的那个版本

如果主项目保存的子模块的commit和子项目的游离的Head不一致，主项目的git status就会显示出这个差异

有两种情况会导致主项目保存的子模块的commit和子模块的Head不一致:

- 子模块的游离Head更新了

  本地游离子模块游离的Head更新，一般是开发者本地对子模块做了修改导致的。如果开发者是误改，可以reset掉错误的修改。如果开发者确实需要修改，那么在子模块的git环境下，git pull，git commit提交到子模块的远端仓库，并且回到主项目中的git环境下，执行`git submodule update --remote`

- 父模块保存的子模块的Commit ID更新了（我们最常遇到的问题）

  出现这种情况的原因，一般是其他人更新了主项目中存储的子模块的commit Id，当你pull远端代码之后，就会互相这种现象。需要执行`git submodule update`，执行该命令后，子模块中的游离Head就会指向和主项目中一致的commit Id

#### git submodule的使用

--------

- 添加引用

- 删除子项目

  ```
  1. 删除.submodule文件
  2. 删除.git目录下, config文件中的子项目对应的引用
  3. 删除.git目录下, module目录对应的子项目
  4. 删除主工程对应的子项目
  5. git add & git commit(主要是避免重新添加子项目引起冲突)
  ```

  

#### git subtree原理

-------





#### git subtree的使用

-----

- 添加源

  ```
  git remote add THSon3 https://github.com/stackjolin/THSon.3.git 
  ```

- 初始化

  ```
  git subtree add --prefix=THFather/THSon3 THSon3 https://github.com/stackjolin/THSon3.git  master
  ```

- pull

  ```
  git subtree pull --prefix=THFather/THSon3 THSon3 https://github.com/stackjolin/THSon3.git  master
  ```

- push

  ```
  git subtree push --prefix=THFather/THSon3 THSon3 https://github.com/stackjolin/THSon3.git master
  ```



#### git subtree push为什么很慢

------

每次执行subtree的push的时候，总会重新为子目录生成新的提交，这就会造成两个问题：

- 每个提交都需要重新计算，因此每次推送都需要把主工程的所有的提交都计算一遍
- 每次push都是重新计算，导致子项目本地和远端的提交记录不一致，关键还没有共同的父级，导致git无法自动解决冲突，需要完全手动修改

注：幸运的是，我们目前的工作流很轻易就避开了这个问题，哈哈哈，因为子项目不是在主项目中维护的



#### 为什么我们要用git submodule 替换掉 git subtree

------

- git submodule对于新手来说的使用成本高
- 目前的团队协作方式是：子项目 X 由小组B维护，主项目 Y 小组A维护，并且子项目，主项目都是有多个并行分支，dev、test、pre。最坑爹的地方，子项目的分支要对应主项目的分支，每次切分支，需要git submodule update，

其实，我们最最希望，对于项目A的同学来说，不需要关注子项目。用git subtree替换git submodule之后的工作流和没有引用子库的工作流是一样，原因就是git submodule是copy而不是引用，我们无需关注任何子项目



#### git submodule VS git subtree

-----

