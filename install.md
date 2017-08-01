####  Linux下IPFS環境搭建
##### 1、安裝go1.8	

```
使用的包：go1.8.3.linux-amd64.tar.gz
tar -C /usr/local -xzf go1.8.3.linux-amd64.tar.gz

$ sudo chown -R root:root ./go
$ sudo mv go /usr/local/
$ sudo vim /etc/profile
export GOROOT=/usr/local/go
export GOPATH=$HOME/work
export PATH=PATH:GOROOT/bin:$GOPATH  /bin
$ sudo source /etc/profile
```



##### 2、安裝和配置Sublime
- Linux下安裝Sublime

  Install GPG key：

  ```
  wget -qO - https://download.sublimetext.com/sublimehq-pub.gpg | sudo apt-key add -
  ```

  Select the channel to use：

  ```
  echo "deb https://download.sublimetext.com/ apt/stable/" | sudo tee /etc/apt/sources.list.d/sublime-text.list
  ```

  Update apt sources and install Sublime Text：

  ```
  sudo apt-get update
  sudo apt-get install sublime-text
  ```

- 安装Package Control：

  Ctrl+`快捷键调出控制台，输入下面的代码回车安装Paackge Control

  ```
  import urllib.request,os; pf = 'Package Control.sublime-package'; ipp = sublime.installed_packages_path(); urllib.request.install_opener( urllib.request.build_opener( urllib.request.ProxyHandler()) ); open(os.path.join(ipp, pf), 'wb').write(urllib.request.urlopen( 'http://sublime.wbond.net/' + pf.replace(' ','%20')).read())
  ```

- 安装gocode

  在終端輸入：

  ```
  go get github.com/nsf/gocode #重启sublime之后就能感受自动Go的自动代码提示了
  ```



##### 3、設置Sublime Build

想要Sublime能够直接build go项目，还须要修改Golang Config。

打开Package Setting -> Golang Config -> Settings-User，输入：

```
{
    "osx": {
        "PATH": "/Users/xxx/go/bin",
        "GOPATH": "/Users/xxx/go"
    },
    "windows": {
        "PATH": "C:\\Users\\xxx\\go\\bin",
        "GOPATH": "C:\\Users\\xxx\\go"
    },
    "linux": {
        "PATH": "/usr/local/go/bin",
        "GOPATH": "/home/xxx/go"
    }
}
```



注：sublime text3 输入中文切換不出來的解决方法：

```
git clone https://github.com/lyfeyaj/sublime-text-imfix.git
cd ~/sublime-text-imfix （前提：解压后的sublime-text-imfix必须在~目录下） 
sudo cp ./lib/libsublime-imfix.so /opt/sublime_text/ 
sudo cp ./src/subl /usr/bin/
最后把sublime都关掉，然后在终端输入subl
```