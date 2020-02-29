## 安装gflag和glog的一些问题总结

1. 安装gflag  

glog对其有依赖, 默认gflag不是动态-fpic编译的, 不支持后续使用动态编译，所以要使用动态编译
```shell
#基础的编译工具依赖
sudo yum install autoconf automake libtool

#下载gflag
git clone https://github.com/gflags/gflags.git
cd gflags
cmake . -DBUILD_SHARED_LIBS=ON
make -j4
sudo make install
```

2. 安装glog  

要注意在64位系统中，不能链接 GLog 生成动态库。需要指名加入-FPIC编译，并引入gflag所在的include和lib地址
```shell
#下载glog
git clone https://github.com/google/glog
cd glog
sh autogen.sh
./configure CPPFLAGS="-I/usr/local/include -fPIC" LDFLAGS="-L/usr/local/lib"
make -j4
sudo make install
```
  
**到这里基本就完成glog的编译和安装了，后续会在glog的基础上做一些升级包括，自定义日志文件滚动方式,按照天来分割日志并循环滚动**