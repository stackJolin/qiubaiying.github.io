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



# OSX系统上，安装make swift protobuf file环境

简介：



#### Installer the protobuf compiler on a Mac

-----

- 下载protobuf

  https://github.com/google/protobuf/releases

- 解压后，进入目录，依次执行如下命令：

  - ./autogen.sh
  - ./configure
  - make

- 如果过程中报错：`autoreconf: failed to run aclocal: No such file or directory`,执行如下命令：

  - brew install aotoconf
  - brew install automake.
  - 继续执行第二步中的操作

- 编译：

  - make check
  - sudo make install
  - which protoc
  - protoc —version





#### protobuf in swift

------

- clone swift pb 工程执行如下命令：

  ```
  git clone https://github.com/apple/swift-protobuf.git
  cd swift-protobuf
  ```

- 切换到最新tag

  ```
  git tag -l
  git checkout tags/1.7.0
  ```

- 编译

  ```
  swift build -c release -Xswiftc -static-stdlib
  ```

- 执行万上面的命令后，在.build/release目录下会生成一个可执行文件'protoc-gen-swfit'，将改文件copy到 `usr/local/bin`目录下

- 命令行执行如下命令即可生成swift的版本的pb文件