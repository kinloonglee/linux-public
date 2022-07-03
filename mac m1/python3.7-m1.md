
## 报pymysql  mysqldb的问题,
是因为

```
import pymysql
pymysql.install_as_MySQLdb()
```
这两行代码,要添加到主项目的__init__文件下面.其它地方都会报错.

## 报python版本的问题,路径的,都是因为没有全局使用python3.7

```python

cd / &&  pyenv global 3.7.11test

```

## 安装arm版本的pyenv
```python
https://laict.medium.com/install-python-on-macos-11-m1-apple-silicon-using-pyenv-12e0729427a9
```

##### 1.Clone the pyenv repo into your home folder:

```
 git clone https://github.com/pyenv/pyenv.git ~/.pyenv
 cd ~/.pyenv && src/configure && make -C src

```
##### 2. Edit your .zshrc and add the following lines at the bottom of the file (macOS 11 comes with zsh as the default shell)

```
export PYENV_ROOT="$HOME/.pyenv" 
export PATH="$PYENV_ROOT/bin:$PATH" 
eval "$(pyenv init --path)" 
eval "$(pyenv init -)"
```

##### 3. Quit your terminal and reopen it. Now pyenv should be activated and you can start to install some Python.

```
$ arch 
arm64
$ which brew 
/opt/homebrew/bin/brew 
$ brew --version 
Homebrew 3.1.11 
Homebrew/homebrew-core (git revision 7c34424687; last commit 2021-06-10) 
Homebrew/homebrew-cask (git revision ab9a64f927; last commit 2021-06-10) 
$ pyenv --version 
pyenv 2.0.1-3-g1706436f
```
##### 4.Install the Python build dependencies for macOS 11

```
brew install openssl readline sqlite3 xz zlib
```
##### 5.Install Python 3.7 on macOS 11 M1 (Apple Silicon)

```
pyenv install 3.7.11


$ pyenv install 3.7.10
python-build: use openssl@1.1 from homebrew
python-build: use readline from homebrew
Downloading Python-3.7.10.tar.xz...
-> https://www.python.org/ftp/python/3.7.10/Python-3.7.10.tar.xz
Installing Python-3.7.10...
python-build: use readline from homebrew
python-build: use zlib from xcode sdk
```

#### 6. pyenv安装python 版本报错,就是因为 安装了intel的homebrew造成的
```
https://github.com/pyenv/pyenv/issues/1877
```

```
export LDFLAGS="-L/opt/homebrew/lib"; export CPPFLAGS="-I/opt/homebrew/include"运行前显式设置pyenv install 3.9.3允许使用 arm64 库/头文件成功安装 arm64。

mac里配置了别名
alias  pyenv="export LDFLAGS="-L/opt/homebrew/lib"; export CPPFLAGS="-I/opt/homebrew/include";pyenv"

但是，只需删除 /usr/local 中的 i386 homebrew 安装（无需明确设置任何标志！）也可以使安装成功。我也刚测试过。

似乎 python 构建可以在 /opt/homebrew/ 中找到 libgettext 库/头文件。问题是，如果这些库也存在于 /usr/local 中，那么构建（错误地）会使用这些库。设置FLAGS明确防止这种情况。
```


## **mac 在vmware pd虚拟机上  查看gateway地址**
  `https://blog.csdn.net/weixin_44528131/article/details/106879350`

  