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



##git submodule & git subtree

git submodule 和 git subtree 是 git 内嵌的 ‘包依赖’ 功能模块。git subtree没有出现之前，git submodule是Git官方推荐的子项目管理方案，在git 1.5.2版本之后。git subtree出现了，相同的，git subtree成了官方努力推荐的子模块管理方案



#### git submodule原理

------





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

#### 为什么我们要用git submodule 替换掉 git subtree

------





#### git submodule VS git subtree

-----

