# 学习使用git，github以及git@oschina

学习使用分布式版本控制系统，主要工作方式：

*  本地开发
*  push 到 github
*  push 到 git@oschina

## 步骤

### 申请github、git.oschina的账号

### 在开发机器上创建key

```shell
ssh-keygen -t rsa -C "xueron@xxxxx.com"
```
key默认保存在~/.ssh/id_rsa中，其中id_rsa是私钥，id_rsa.pub是公钥。

id_rsa,id_dsa 是linux下ssh客户端默认的key的文件名称，如果需要配置多个不同的key，并且在ssh-keygen生成key的时候，使用到了其他文件名称保存，则需要修改ssh的配置文件，让ssh客户端认识你新生成的key：/etc/ssh/ssh_config，将新的文件名称告诉ssh，让他认识：

```conf
IdentityFile ~/.ssh/identity
IdentityFile ~/.ssh/id_rsa
IdentityFile ~/.ssh/id_dsa
IdentityFile ~/.ssh/git@github.com
```
