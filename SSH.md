# Linux（Ubuntu ）中配置 SSH

## 一、在 Ubuntu 上启用 SSH

1. 安装openssh-server软件包

   ```bash
   sudo apt update
   sudo apt install openssh-server
   ```

2. 安装完成后，SSH 服务将自动启动，验证 SSH 是否正在运行

   ```bash
   sudo systemctl status ssh
   ```

3. 若开启了UFW防火墙，则添加通行规则

   ```bash
   sudo ufw allow ssh
   ```

## 二、使用 SHH 连接工具进行连接即可

​	**常用SSH工具**

* [Visual Studio Code](https://code.visualstudio.com/)
* [Tabby](https://github.com/Eugeny/tabby)
* [PuTTY](https://www.chiark.greenend.org.uk/~sgtatham/putty/)

## 三、免密登录

**将本机公钥`/.ssh/id_rsa.pub`的内容拷贝到远程主机`/.ssh/authorized_keys`文件里，每次登录就不需要使用密码了。**

1. 查看本机公钥

   ```bash
   cat ~/.ssh/id_rsa.pub
   ```

2. 生成本机`SSH`密钥

   *若已有 ssh 密钥再次生成则会将原来的覆盖，已经配置过 git 则无需再次生成*

   ```bash
   ssh-keygen -t rsa
   ```

3. 发送公钥至远程主机

   ```bash
   # 将本地公钥拷贝到远程主机：IP地址为ip，用户名为username下 /.ssh/authorized_keys 文件里
   ssh-copy-id username@ip
   # 运行后输入用户密码即可上传
   ```

   *Windows系统下没有`ssh-copy-id`命令，可以使用`Git Bash`运行后输入密码，或者直接复制粘贴到`/.ssh/authorized_keys`文件里*

4. 发送成功后登录远程主机确认

   ```bash
   cat ~/.ssh/authorized_keys
   ```


## 四、在 Ubuntu 上禁用 SSH

**在 Ubuntu 系统上禁用 SSH 服务器，简单停止 SSH 即可**

   ```bash
# 禁用 SSH 服务器
sudo systemctl disable --now ssh

# 启用 SSH 服务器
sudo systemctl enable --now ssh
   ```

## 
