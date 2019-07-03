# Aria2Gui-Mod

Releases中有我修改好的版本可以直接下载使用

原作者的中文文档
[中文文档](https://www.hguandl.com/post/8f0b723a.html)

## Introduction
Some patches to aria2. Remove connection limit and fix building on macOS.

- Enable resuming to download by default
- Set default concurrent downloads to 128
- Set default max connections to per server to 64 and remove the limit of 16 before
- Set default minimum split size to 1M
- Set default timeout to 30s
- Change the minimum unit of piece length to 1K
- Set default retry times to 2
- Set default split pieces to 128
- Disable checking certificates by default
- Fix defination of `std::make_unique` to build on maxOS.

## 中文Introduction
- 默认开启断点续传
- 默认同时下载数改为 128
- 默认同服务器连接数改为 64，解除了之前 16 的限制
- 默认最小分片大小改为 1M
- 默认超时改为 30s
- 分片大小的最小单位改为精确到 KB
- 默认重试次数改为 2 次
- 默认分片数量改为 128
- 默认不检查证书（单纯为了下载，事实上存在安全隐患）
- 修改了源码中对于 std::make_unique 的定义，使其在 macOS 上也能正常编译

## Usage
### Get the source code
You can download from [releases](https://github.com/aria2/aria2/releases) or [git](https://github.com/aria2/aria2).

```bash
$ git clone https://github.com/aria2/aria2.git
```

### Apply the patches from this repo
```bash
$ git clone https://github.com/hguandl/aria2-patch.git
$ cd aria2
$ patch -p1 < ../aria2-patch/aria2-fast.patch
```

### Build
For Linux users, just see [How to build](https://github.com/aria2/aria2#how-to-build).

For macOS users, please follow these steps:

1. Install dependencies from [Homebrew](https://brew.sh). To use `gettext` binary, you also need to add it to `$PATH`.
```bash
$ brew install autoconf automake libtool gettext pkg-config
$ export PATH="/usr/local/opt/gettext/bin:$PATH"
```
2. Configure and build
```bash
$ autoreconf -i
$ ./configure ARIA2_STATIC=yes CXXFLAGS="-O2 -std=c++14" --prefix=/usr/local
$ make install
```

## 感谢以下几位作者的开源与修改
- https://www.52pojie.cn/thread-602534-1-1.html
- https://github.com/hguandl/aria2-patch
- https://github.com/yangshun1029/aria2gui
