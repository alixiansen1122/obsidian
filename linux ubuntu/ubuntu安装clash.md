![[Pasted image 20260414165854.png]]
ubuntu属于debian系
https://github.com/clash-verge-rev/clash-verge-rev  github发布页
![[Pasted image 20260414170426.png]]
sudo apt install -y ./Clash.Verge_x.x.x-_xxx.deb

3206398901 moji :   https://47.242.128.61:5000/api/v1/client/subscribe?token=6a5dc0530112c417db06724d5c5e62e7

export http_proxy="http://127.0.0.1:7890" export https_proxy="http://127.0.0.1:7890"  设置代理

sudo bash -c 'echo -e "Acquire::http::Proxy \"http://127.0.0.1:7890\";\nAcquire::https::Proxy \"http://127.0.0.1:7890\";" > /etc/apt/apt.conf.d/proxy.conf'    



简单来说，它会在系统的 `apt` 配置目录中新建（或覆盖）一个文件，把你的代理地址（`127.0.0.1:7890`）写进去，从而强制 `apt` 在以后更新或下载软件时，都通过这个代理进行网络请求。

为了让你更清楚它是怎么运作的，我们可以把这行长长的命令拆解开来看：

### 核心拆解

- **`sudo`**：以管理员（root）权限执行命令。因为你要修改系统级别的配置文件目录（`/etc/`），普通用户没有权限，必须加 `sudo`。
    
- **`bash -c '...'`**：启动一个新的 bash shell 来执行单引号 `''` 里面的整段命令。
    
    - _为什么要这样写？_ 因为如果直接写 `sudo echo "内容" > 文件`，`sudo` 只能赋予 `echo` 管理员权限，但后面的重定向符号 `>` 依然是普通用户权限，会导致“权限不够”的报错。用 `bash -c` 包起来，就可以让“生成内容”和“写入文件”这两个动作都在管理员权限下完成。
        
- **`echo -e`**：输出一段文本。`-e` 参数的作用是让 `echo` 能够识别特殊字符，比如后面紧跟的 `\n`（换行符）。
    
- **`"Acquire::http::Proxy \"http://127.0.0.1:7890\";\nAcquire::https::Proxy \"http://127.0.0.1:7890\";"`**：这是实际要写入文件的内容。
    
    - `\"` 是转义字符，用来在文本里保留真正的双引号。
        
    - `\n` 是换行符，告诉系统在这里另起一行。
        
- **`>`**：重定向符号。意思是“把前面生成的内容，不要显示在屏幕上，而是写进后面的文件里”。如果文件不存在就创建它，如果已存在就覆盖它。
    
- **`/etc/apt/apt.conf.d/proxy.conf`**：目标文件的路径。`/etc/apt/apt.conf.d/` 是 `apt` 读取额外配置的默认目录，`proxy.conf` 是我们给这个代理配置文件起的名字（名字叫什么其实无所谓，只要在这个目录下，以 `.conf` 结尾，`apt` 就能识别）。
    

---

### 最终结果

当你在终端敲下并回车执行完这条命令后，系统里就会多出一个名为 `/etc/apt/apt.conf.d/proxy.conf` 的文件，它的真实内容长这样：

Plaintext

```
Acquire::http::Proxy "http://127.0.0.1:7890";
Acquire::https::Proxy "http://127.0.0.1:7890";
```

这正是 `apt` 能够读懂的代理配置语法。之后无论你运行多少次 `sudo apt update`，它都会自动走这个代理了。