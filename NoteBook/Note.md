# NoteBook
## Arm架构CentOS7换阿里源
* 进入yum.repo.d  
```bash
cd /etc/yum.repos.d/
```
* 备份原yum源(或者都删除)
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
yum clean dbcache
yum clean metadata
yum clean rpmdb
yum clean headers
yum clean all

rm -rf /var/cache/yum/timedhosts.txt
rm -rf /var/cache/yum/*

yum makecache
```

* 若出现 `Couldn't open file /etc/pki/rpm-gpg/RPM-GPG-KEY-EPEL-7`  
  - 在使用`yum install`的时候，偶尔会碰见这样的错误：   
    `Couldn’t open file /etc/pki/rpm-gpg/RPM-GPG-KEY-EPEL-7`
  - `/etc/yum.repos.d` 目录下有关于`yum repository`的配置文件中列有如下的`GPG key`:   
    `key=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-EPEL-7`
  - 这会告诉YUM，这个repository的`GPG key`存在于磁盘上。而当YUM在路径 `/etc/pki/rpm-gpg` 下找不到这个 GPG key 的时候，就会报如上的错误了。
  - 解决方案：
    ```bash
    cd /etc/pki/rpm-gpg
    wget https://archive.fedoraproject.org/pub/epel/RPM-GPG-KEY-EPEL-7
    ```
