# NoteBook
## Arm架构CentOS7换阿里源
* 进入yum.repo.d  
```bash
cd /etc/yum.repos.d/
```
* 备份原yum源  
```bash
mkdir yum-back
```
```bash
mv CentOS-* yum-back/
```
* yum替换源为阿里源(文件在同目录下 ./Arm-CentOS7-Base 文件夹中)
```bash
vim CentOS-Base.repo
```
* 继续修改epel.repo(文件在同目录下 ./Arm-CentOS7-Base 文件夹中)
```bash
vim epel.repo
```
* 替换认证秘钥(文件在同目录下 ./Arm-CentOS7-Base 文件夹中)
```bash
cd /etc/pki/rpm-gpg/
```
```bash
vim RPM-GPG-KEY-CentOS-7
```  
* 继续修改RPM-GPG-KEY-CentOS-7-aarch64(文件在同目录下 ./Arm-CentOS7-Base 文件夹中)
```bash
vim RPM-GPG-KEY-CentOS-7-aarch64
```
* 生成缓存
```bash
yum makecache
```  
