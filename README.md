# github + ssh 使用
1. 本地开启 ssh-agent
	```shell
	$ eval `ssh-agent -s`
	```

2. 检查 ssh-agent 管理的密钥
	```shell
	$ ssh-add -L
	```
3. 如果需要，创建一个新的密钥
	```shell
	$ ssh-keygen -t ed25519 -C "your_email@example.com"
	```
	-t 指明目标，因此生成的密钥的私钥名字是 id_ed25519 对应公钥是 id_ed25519.pub
		私钥交给 ssh-agent 管理，公钥交给 github
	-C 指明密钥对应的持有人的电子邮件地址
4. 将密钥添加到 ssh-agent中
	```shell
	$ ssh-add ~/.ssh/id_ed25519
	```
5. 将密钥添加到 github 中
	```shell
	$ clip < ~/.ssh/id_ed25519.pub
	```
	clip 将接收到的内容复制到剪切板
	< 表示信息流向，id_ed25519.pub 的内容全部输入到 clip

	打开 github 的 setting，创建一个新的 ssh key。将剪切板内容添加。
6. 检查是否能成功连接
	```shell
	$ ssh -T git@github.com
	```
7. 使用 ssh 克隆
	```shell
	$ git clone url
	```
	这里的 url 是仓库的下载方式中，ssh 那一种给出的地址
8. 设置本地仓库的 ssh 上游地址
	```shell
	$ git remote set-url origin git@github.com:username/your-repository.git
	```
	
[reference](https://gist.github.com/xirixiz/b6b0c6f4917ce17a90e00f9b60566278)
