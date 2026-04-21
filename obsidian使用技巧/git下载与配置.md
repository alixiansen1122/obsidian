## 1.首先在gitee注册账号
## 2.下载Git for Windows
## 3.在gitee创建仓库，私有，不要进行任何初始化，要纯空
## 4.git初始化
	### 1. 打开你的 **Obsidian 笔记文件夹**（在文件管理器里打开）。
	1. 在空白处 **右键** -> 选择 **Git Bash Here**。
	2. 会出现一个黑色的命令框，**依次复制粘贴**下面的命令（一行一行执行，回车确认）：
	    - **命令1（告诉 Git 你是谁）：**  
	        (注意把双引号里的内容改成你自己的)  
	        git config --global user.name "你的名字"
	    - **命令2（告诉 Git 你的邮箱）：**  
	        git config --global user.email "你的邮箱@example.com"
	    - **命令3（初始化）：**  
	        git init  
	        (这时候你会发现文件夹里多了一个隐藏的 .git 文件夹)
	    - **命令4（添加云端地址）：**  
	        git remote add origin 刚刚你复制的Gitee地址
	    - **命令5（第一次手动上传）：**  
	        git add .  
	        git commit -m "first commit"  
	        git push -u origin master
	    注意：执行最后一步 git push 时，可能会弹出一个框让你输入 Gitee 的账号和密码，输入即可。
	##### 如果最后显示 Branch 'master' set up to track remote branch... 或者没有报错，恭喜你！**最难的部分搞定了！**
## 5.安装并且初始化成功则进行配置
![[Pasted image 20251204115336.png|500]]![[企业微信截图_17648235541379.png|400]]![[企业微信截图_17648236579952.png|400]]![[企业微信截图_17648236641086.png|400]]![[企业微信截图_17648236834885.png|350]]![[企业微信截图_17648236911593.png|400]]