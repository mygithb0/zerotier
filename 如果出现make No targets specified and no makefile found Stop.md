# 安装mysql时遇到make: *** No targets specified and no makefile found. Stop.

原创

[mob649e81593bda](https://blog.51cto.com/u_16175453) 2023-09-11 09:30:24

**_文章标签_ [MySQL](https://blog.51cto.com/search/result?q=MySQL) [mysql](https://blog.51cto.com/topic/mysql-2.html) [编译环境](https://blog.51cto.com/topic/bianyihuanjing.html)** **_文章分类_ [MySQL](https://blog.51cto.com/nav/mysql) [数据库](https://blog.51cto.com/nav/database)** **_阅读数_**845****

## 安装MySQL时遇到 “make: *** No targets specified and no makefile found. Stop.” 错误的解决方法

在进行软件安装的过程中，我们有时候会遇到各种各样的错误。其中之一就是在安装MySQL时出现 “make: *** No targets specified and no makefile found. Stop.” 错误。这个错误通常是由于缺少必要的依赖库或者编译环境不完整导致的。本文将为您介绍如何解决这个问题，并提供相应代码示例。

### 1. 确认编译环境是否完整

在编译安装MySQL之前，我们需要确保编译环境是完整的。首先，我们需要确认系统中是否已经安装了必要的编译工具，比如 `make`、`gcc` 等。我们可以通过以下命令来检查：

```shell
which make
which gcc
```

如果没有安装，我们可以通过以下命令来安装：

```shell
sudo apt-get install make
sudo apt-get install gcc
```

此外，我们还需要确认系统中是否已经安装了必要的依赖库，比如 `libncurses5-dev`、`libssl-dev` 等。我们可以通过以下命令来检查：

```shell
dpkg -s libncurses5-dev
dpkg -s libssl-dev
```

如果没有安装，我们可以通过以下命令来安装：

```shell
sudo apt-get install libncurses5-dev
sudo apt-get install libssl-dev
```

### 2. 下载MySQL源码

在确认编译环境完整之后，我们需要下载MySQL的源码。我们可以从MySQL官方网站上下载最新版本的源码包，也可以使用以下命令自动下载：

```shell
wget 
```

### 3. 解压源码包

下载完成后，我们需要将源码包进行解压。我们可以使用以下命令解压：

```shell
tar -zxvf mysql-8.0.23.tar.gz
```

解压完成后，进入解压后的目录：

```shell
cd mysql-8.0.23
```

### 4. 配置MySQL编译选项

在编译之前，我们需要根据自己的需求进行一些配置。MySQL提供了一个 `cmake` 工具来进行配置。我们可以使用以下命令进行配置：

```shell
cmake . -DCMAKE_INSTALL_PREFIX=/usr/local/mysql -DMYSQL_DATADIR=/usr/local/mysql/data -DWITH_INNOBASE_STORAGE_ENGINE=1 -DWITH_ARCHIVE_STORAGE_ENGINE=1 -DWITH_BLACKHOLE_STORAGE_ENGINE=1 -DENABLE_DOWNLOADS=1 -DWITH_BOOST=boost -DWITH_SSL=system -DWITH_TAOCRYPT=0
```

在执行这个命令之前，我们需要确保系统已经安装了 `cmake` 工具。我们可以使用以下命令来安装：

```shell
sudo apt-get install cmake
```

以上命令中，`-DCMAKE_INSTALL_PREFIX` 参数指定了MySQL的安装路径，`-DMYSQL_DATADIR` 指定了MySQL的数据存储路径，`-DWITH_INNOBASE_STORAGE_ENGINE`、`-DWITH_ARCHIVE_STORAGE_ENGINE`、`-DWITH_BLACKHOLE_STORAGE_ENGINE` 分别指定了是否启用InnoDB、Archive、Blackhole等存储引擎。根据自己的需求进行配置。

### 5. 编译和安装MySQL

配置完成后，我们可以使用以下命令进行编译和安装：

```shell
make
sudo make install
```

在编译过程中，如果出现 “make: *** No targets specified and no makefile found. Stop.” 错误，通常是由于缺少依赖库或者配置错误导致的。我们可以根据错误信息来查找原因，并进行相应的修复。

### 6. 配置MySQL环境变量

安装完成后，我们需要将MySQL的可执行文件路径添加到系统的环境变量中，以便我们可以在任意位置使用MySQL命令。打开 `~/.bashrc` 文件，添加以下内容：

```shell
export PATH=$PATH:/usr/local/mysql/bin
```

保存文件后，使用以下命令使配置生效：