
# Install EOS in mate 

### 1、 install cmake 
### 2、install boost
```sh
sudo apt-get install mpi-default-dev　　#安装mpi库  
sudo apt-get install libicu-dev　　　　　#支持正则表达式的UNICODE字符集   
sudo apt-get install python-dev　　　　　#需要python的话  
sudo apt-get install libbz2-dev　　　　#如果编译出现错误：bzlib.h: No such file or directory
```
注意，复制粘贴的时候，不要复制命令后面的空格，这样会导致一个无法定位软件包的错误.

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
