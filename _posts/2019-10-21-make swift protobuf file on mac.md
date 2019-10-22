---
layout:     post
title:      make swift protobuf file
subtitle:   make swift protobuf file
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





#### 生成protoc-gen-swift可执行文件

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

注：可以通过brew安装，简单的执行命令`brew install swift-protobuf`

#### 生成protoc-gen-swiftgrpc可执行文件

------

```
git clone git clone https://github.com/grpc/grpc-swift.git
cd grpc-swift
make plugin
```

执行完上面命令会生成一个文件protoc-gen-swift，将该文件copy到 `usr/local/bin`目录下



#### 根据proto文件，生成swift版本的代码

-----

```
protoc mockcsclient_mockcsclient.proto --swift_out=commen --swiftgrpc_out=Client=true,Server=false:commen
```