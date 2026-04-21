### 第一步：在 Linux 上检查 Samba 服务状态

```
# 1. 检查 Samba 是否已安装
sudo apt install samba samba-common-bin

# 2. 检查 Samba 服务状态
sudo systemctl status smbd

# 如果未运行，启动 Samba
sudo systemctl start smbd
sudo systemctl enable smbd
```

### 第二步：创建和配置共享文件夹

```
# 1. 检查共享文件夹是否存在（从您的终端路径看，应该存在）
ls -la ~/T553_NA/

# 2. 给文件夹设置适当的权限
sudo chmod 777 ~/T553_NA/  # 临时测试用，生产环境请设置更安全的权限

# 3. 备份原始 Samba 配置
sudo cp /etc/samba/smb.conf /etc/samba/smb.conf.backup

# 4. 编辑 Samba 配置文件
sudo nano /etc/samba/smb.conf
```

在 `smb.conf`文件末尾添加以下配置：
```
[T553_NA]
   path = /home/ssm/T553_NA
   browseable = yes
   read only = no
   guest ok = no
   create mask = 0775
   directory mask = 0775
   valid users = ssm
```

### 第三步：添加 Samba 用户并重启服务
```
# 1. 添加您的用户到 Samba（会提示设置密码）
sudo smbpasswd -a ssm
# 输入两次密码（建议与系统密码不同）

# 2. 重启 Samba 服务
sudo systemctl restart smbd

# 3. 检查防火墙是否阻止了 Samba
sudo ufw allow samba
# 或者临时关闭防火墙测试
sudo ufw disable
```
### 第五步：在 Windows 上重新连接

1. **使用 IP 地址直接访问**：
    
    - 打开文件资源管理器
        
    - 在地址栏输入：`\\192.168.92.128`
        
    - 按 Enter，应该能看到共享文件夹列表
        
    
2. **映射网络驱动器**：
    
    - 再次尝试映射，使用：`\\192.168.92.128\T553_NA`
        
    - 当提示输入凭据时：
        
        - 用户名：`ssm`（或 `192.168.92.128\ssm`）
            
        - 密码：您设置的 Samba 密码