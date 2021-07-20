为了支持cpp11，gcc版本要4.9+，所以一些比较老的系统比如centos7.6，gcc默认4.8.5，是要升级gcc/g++的。



Ubuntu18 通过apt方式安装cmake的版本是 3.10.2。对grpc来说，太低了。所以我们直接安装目前的最高版本。
cmake3.21 目前是最新版本

注意如果卸载旧cmake，会把ROS包里的很多东西卸掉，装完新版cmake后需要重装ROS（本人踩了这坑是按这个方式做的），或者直接升级cmake而非卸载安装。



安装zlib

```bash
wget http://www.zlib.net/zlib-1.2.11.tar.gz
tar -xvf zlib-1.2.11.tar.gz
cd zlib-1.2.11/
./configure
make
sudo make install
```



选择一个目录来保存本地安装的软件包。此页面假定环境变量MY_INSTALL_DIR包含此目录路径。例如：

```bash
export MY_INSTALL_DIR=$HOME/.local
```

确保目录存在：

```bash
mkdir -p $MY_INSTALL_DIR
```

将本地`bin`文件夹添加到您的路径变量，例如：

```bash
export PATH="$MY_INSTALL_DIR/bin:$PATH"
```





#### 拉取grpc ,指定版本v1.12.0

```bash
git clone https://gitee.com/niubucai/grpc.git
cd grpc/ 
git tag 
git checkout v1.12.0
git submodule sync 
git submodule update --init
```



将protoc更新到v3.6.1 make -j4是多和编译，-j后面的参数根据当前系统配置加快编译

```bash
cd third_party/protobuf
git tag
git checkout v3.6.1
./autogen.sh 
./configure
sudo make -j4
sudo make install
sudo ldconfig     
protoc --version  
```





编译安装grpc 加参数 HAS_SYSTEM_PROTOBUF=false

```
cd ../../ # 这里是grpc的目录
make HAS_SYSTEM_PROTOBUF=false 
sudo make install 
```





修改下.gitmodules文件，内容如下，如果自己从GitHub上复制了这些库，也可以用自己的拷贝。

```bash
[submodule "third_party/zlib"]
        path = third_party/zlib
        url = https://gitee.com/niubucai/zlib.git
        # When using CMake to build, the zlib submodule ends up with a
        # generated file that makes Git consider the submodule dirty. This
        # state can be ignored for day-to-day development on gRPC.
        ignore = dirty
[submodule "third_party/protobuf"]
        path = third_party/protobuf
        url = https://gitee.com/niubucai/protobuf.git
[submodule "third_party/googletest"]
        path = third_party/googletest
        url = https://gitee.com/niubucai/googletest.git
[submodule "third_party/benchmark"]
        path = third_party/benchmark
        url = https://gitee.com/niubucai/benchmark
[submodule "third_party/boringssl"]
        path = third_party/boringssl
        url = https://gitee.com/niubucai/boringssl.git
[submodule "third_party/boringssl-with-bazel"]
        path = third_party/boringssl-with-bazel
        url = https://gitee.com/niubucai/boringssl.git
[submodule "third_party/re2"]
        path = third_party/re2
        url = https://gitee.com/niubucai/re2.git
[submodule "third_party/cares/cares"]
        path = third_party/cares/cares
        url = https://gitee.com/niubucai/c-ares.git
        branch = cares-1_12_0
[submodule "third_party/bloaty"]
        path = third_party/bloaty
        url = https://gitee.com/niubucai/bloaty.git
[submodule "third_party/abseil-cpp"]
        path = third_party/abseil-cpp
        url = https://gitee.com/niubucai/abseil-cpp.git
        branch = lts_2020_02_25
[submodule "third_party/envoy-api"]
        path = third_party/envoy-api
        url = https://gitee.com/niubucai/data-plane-api.git
[submodule "third_party/googleapis"]
        path = third_party/googleapis
        url = https://gitee.com/niubucai/googleapis.git
[submodule "third_party/protoc-gen-validate"]
        path = third_party/protoc-gen-validate
        url = https://gitee.com/niubucai/protoc-gen-validate.git
[submodule "third_party/udpa"]
        path = third_party/udpa
        url = https://gitee.com/niubucai/udpa.git
[submodule "third_party/libuv"]
        path = third_party/libuv
        url = https://gitee.com/niubucai/libuv.git
[submodule "third_party/opencensus-proto"]
        path = third_party/opencensus-proto
        url = https://gitee.com/niubucai/opencensus-proto.git
[submodule "third_party/gflags"]
        path = third_party/gflags
        url = https://gitee.com/niubucai/gflags.git
```





跑示例

```bash
cd example/cpp/helloworld
mkdir -p cmake/build
pushd cmake/build
sudo make
./greeter_server
```

新建一个终端

```bash
cd example/cpp/helloworld
./greeter_client
Greeter received: Hello world
```





```bash
/grpc/test/distrib/cpp$ sudo ./run_distrib_test_cmake.sh
```

如果跑不起来注释一部分