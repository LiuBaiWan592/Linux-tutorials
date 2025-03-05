# 配置 Ubuntu 中 UFW 防火墙

1. 查看防火墙状态：

   ```bash
   sudo ufw status
   # inactive：关闭不活动状态
   # active：开启激活状态
   ```

   *这将显示当前防火墙规则的状态，包括是否启用和允许的规则*

2. 开启防火墙：

   ```bash
   sudo ufw enable
   ```

   *启用防火墙后，它将按照默认规则开始工作，通常会拒绝所有传入连接，但允许所有传出连接*

3. 关闭防火墙：

   ```bash
   sudo ufw disable
   ```

   *关闭防火墙后，所有传入和传出的连接将被允许，不再受到防火墙的限制*

4. 常用的防火墙命令：

   ```bash
   # 外来访问默认 允许/拒绝
   sudo ufw default allow/deny
   
   # 允许/拒绝 访问20端口
   sudo ufw allow/deny 20
   # 允许/拒绝 tcp（或udp）封包访问20端口
   sudo ufw allow/deny 20/tcp
   
   # 从/etc/services中找到对应service的端口，进行过滤
   sudo ufw allow/deny servicename
   # 例如：
   sudo ufw allow ssh
   
   # 允许自192.168.0.0/24的tcp封包访问本机的20端口。
   sudo ufw allow proto tcp from 192.168.0.0/24 to any port 20
   
   # 删除以前定义的"允许/拒绝访问20端口"的规则
   sudo ufw delete allow/deny 20:
   ```