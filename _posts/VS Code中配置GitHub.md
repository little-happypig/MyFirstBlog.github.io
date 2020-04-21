# vscode中配置Github

## 1. 配置Git

安装最新版git后，命令行输入

git config user.name '你的名字' -g
git congif user.email '你的邮箱' -g

## 2. Github设置

在GitHub中新建一个空仓库（新项目）

确认后显示ssh地址

首先在本地新建一个目录，这里git的操作要在这个新建的目录下操作（在这个文件夹中右键选择git Bash here），在Git Bash中依次运行下列代码
echo "# vscode-demo" >> README.md
git init
git add README.md
git commit -m "first commit"
git remote add origin git@github.com:plusczh/vscode-demo.git
git push -u origin master
如果在输出最后一行报错fatal:Could not read from remote repository
则需要设置SSH key
右上角个人图标---Settings---左边栏SSH and GPG keys---New SSH key
title随便取，密码设置如下

执行这个命令（在git bash中）

按下三次回车，看到泡泡一样的东西出现，说明安装成功
再键入cat ~/.ssh/id_rsa.pub，得到的一串字符输入到新建SSH时的密码栏
设置好SSH key，重新运行上面那段命令，刷新Github页面就能看到仓库名

## 3. vscode设置

在vscode中打开那个在github中库托管的文件夹

步骤：

打开源代码管理栏
输入提交信息（注释）
提交
点开选择推送
当检测到有文件更改时更改栏才会有显示，才可以提交
push的过程是不用输入密码的，如果想有更好的git管理体验，可以在插件商店寻找相关插件。
