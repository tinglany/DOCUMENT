
# Install EOS in mate （standalone mode）

### 1、 install cmake 
### 2、install boost
```sh
sudo apt-get install mpi-default-dev　　#安装mpi库  
sudo apt-get install libicu-dev　　　　　#支持正则表达式的UNICODE字符集   
sudo apt-get install python-dev　　　　　#需要python的话  
sudo apt-get install libbz2-dev　　　　#如果编译出现错误：bzlib.h: No such file or directory
```
注意,复制的命令后面不要有空格，这样会导致一个无法定位软件包的错误.

安装失败统一的办法：
```sh
sudo apt-get update
```
下载boost
http://sourceforge.net/projects/boost/files/latest/download?source=dlp

下载好了以后，解压 .bz2 文件：
```sh
tar -jxvf xx.tar.bz2
```
解压之后，进入解压目录，执行：
```sh
./bootstrap.sh
sudo ./b2
sudo ./b2 install
```
测试下：
```sh
#include<iostream>
#include<boost/bind.hpp>
using namespace std;
using namespace boost;
int fun(int x,int y){return x+y;}
int main(){
    int m=1;int n=2;
    cout<<boost::bind(fun,_1,_2)(m,n)<<endl;
    return 0;
}
```
编译：
```sh
g++ test.cpp -o test
./test  #执行输出3
```

注 : boost的安装时间还是很长的，单核的虚拟机上面 30 min 左右

### 3 isntall OpenSSL
```sh
sudo apt-get isntall openssl
```
### 4 install secp256k1-zkp
```sh
1.  git	clone https://github.com/cryptonomex/secp256k1-zkp.git	
2.  cd secp256k1-zkp	
3.  ./autogen.sh	
4.  ./configure	
5.  make	
6.  sudo make install
```
### install LLVM
```sh
brew install llvm	
```
编译 WASM 编译环境:
```
```sh
1.  mkdir ~/wasm-compiler
2.  cd ~/wasm-compiler
3.  git clone --depth 1 --single-branch --branch release_40 https://github.com/llvm-mirror/llvm.git
4.  cd llvm/tools
5.  git clone --depth 1 --single-branch --branch release_40 https://github.com/llvm-mirror/clang.git
6.  cd ..
7.  mkdir build	
8.  cd build	
9.  cmake -G "Unix Makefiles" -DCMAKE_INSTALL_PREFIX=.. -DLLVM_TARGETS_TO_BUILD= -DLLVM_EXPERIMENTAL_TARGETS_TO_BUILD=WebAssembly -DCMAKE_BUILD_TYPE=Release ../	
10. make -j4 install
```
prepare work end.
### 升级cmake
(如mate自带cmake3.5低版本编译EOS时会报错)
从cmake官网下载source distributions
然后解压安装：
```sh
# tar -zxvf cmake-3.8.2.tar.gz
# ./bootstrap
# make
# make isntall
# cmake -version
```


