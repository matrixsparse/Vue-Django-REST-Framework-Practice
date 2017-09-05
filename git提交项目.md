## git提交项目到github
```bash
sparsematrix:~ matrix$ ssh-keygen -t rsa
Generating public/private rsa key pair.
Enter file in which to save the key (/Users/matrix/.ssh/id_rsa):
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
Your identification has been saved in /Users/matrix/.ssh/id_rsa.
Your public key has been saved in /Users/matrix/.ssh/id_rsa.pub.
The key fingerprint is:
SHA256:qQg7q/JGd4JcCl7mStP69X9Ju1Rdhmj5heMoVI7cCiQ matrix@sparsematrix.local
The key's randomart image is:
+---[RSA 2048]----+
|      E .   .    |
|       o . = o o |
|        . + * + +|
|.  o.    + o +.+.|
|.o*+    S o ..o. |
| +==o...   o.    |
|..*..+.   ..o    |
|.o.o. .   .+     |
|o++.   ......    |
+----[SHA256]-----+
```
```bash
点击右上角的 New SSH key 按钮，把 id_rsa.pub 公钥文件里的内容复制粘贴进去就可以了
```
![](http://ww1.sinaimg.cn/large/dc05ba18gy1fj4zzz2e6ej21a80ewn00.jpg)
```bash
SSH key 添加成功之后，输入 ssh -T git@github.com 进行测试，如果出现以下提示证明添加成功了
```
![](http://ww1.sinaimg.cn/large/dc05ba18gy1fj4zzzfnfwj21s00440wk.jpg)
```bash
sparsematrix:~ matrix$ ssh -T git@github.com
Warning: Permanently added the RSA host key for IP address '192.30.255.113' to the list of known hosts.
Hi matrixsparse! You've successfully authenticated, but GitHub does not provide shell access.
```
### git初始化
```bash
sparsematrix:Desktop matrix$ cd VueDRF/
```
```bash
sparsematrix:Vue+Django Restful Framework matrix$ git init
Initialized empty Git repository in /Users/matrix/Desktop/Vue+Django Restful Framework/.git/
```
```bash
sparsematrix:Vue+Django Restful Framework matrix$ git add *
```
### git提交
```bash
sparsematrix:Vue+Django Restful Framework matrix$ git commit -m "first commit"
```
```bash
sparsematrix:Vue+Django Restful Framework matrix$ git remote add origin git@github.com:matrixsparse/Vue-Django-REST-Framework-Practice.git
```
```bash
sparsematrix:Vue+Django Restful Framework matrix$ git push -u origin master
```

