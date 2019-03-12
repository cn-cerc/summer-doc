# Github建立SSH安全链接
#### 1. 创建Github账号的公私钥
```
ssh-keygen -t rsa -C "[your github Email]"
```
#### 2. 查看创建好的公钥并拷贝
```
cat ~/.ssh/id_rsa.pub
```
拷贝公钥
#### 3. 在你的账号中添加公钥
你的头像——settings——SSH and GPG keys——New SSH Key
#### 4. 测试
ssh -T git@github.com

