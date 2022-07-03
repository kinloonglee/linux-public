## 安装bash_completions后,报错

安装bash_completion后,在zshrc中配置生效后,报如下错误:
(3.7.11test) lijinlong@li ~ % source ~/.zshrc                        
zsh compinit: insecure directories, run compaudit for list.



解决方法:
```shell
compaudit
chmod g-w /usr/local/share/zsh
chmod g-w /usr/local/share/zsh/site-functions
```
