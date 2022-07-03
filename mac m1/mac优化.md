# mac的启动台修改数量

```

# 设置列数
defaults write com.apple.dock springboard-columns -int 10
# 设置行数
defaults write com.apple.dock springboard-rows -int 6
# 重启 Dock 生效
killall Dock
```

# mac  m1  vmware查看gateway网关ip配置  nat.conf
```
https://blog.csdn.net/weixin_44528131/article/details/106879350

cd /Library/Preferences/VMware\ Fusion/ 
vim nat.conf
IP=192.168.1.2
```