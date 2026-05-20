1.ssh进行绑定
git config --global user.name "你的名字或昵称"
git config --global user.email "你的邮箱@example.com"
ls -la  **详细列出当前目录下的所有文件和文件夹（包括隐藏文件）**。
	T553_NA:vim config
		Host gerrit.sikey.com.cn
		             KexAlgorithms +diffie-hellman-group1-sha1
		  HostKeyAlgorithms +ssh-rsa
		    PubkeyAcceptedKeyTypes +ssh-rsa
		User shishimao
		Port 29418
		Hostname  192.168.110.50
		Host 192.168.110.50
		             KexAlgorithms +diffie-hellman-group1-sha1
		  HostKeyAlgorithms +ssh-rsa
		    PubkeyAcceptedKeyTypes +ssh-rsa
		User shishimao
		Port 29418
ssh-keygen -t rsa -b 4096 -C "shishimao@sikey.com.cn"
cat id_rsa.pub
~/repo init -u ssh://gerrit.sikey.com.cn:29418/git/platform/manifest -q -b sikey_master -m sikey/T553U_MASTER_20251218.xml   路径调用repo
![[Pasted image 20260414190031.png]]
