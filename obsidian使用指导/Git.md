### 本地文件上传到 github 步骤
[如何将本地新项目上传到git(Mac端) - 简书](https://www.jianshu.com/p/2e4c078602a1)

初始化本地仓库
```js
git init
```

Initialized empty Git repository in /Users/carrot/carrotFile/Knowledge/.git/
这不是一个错误，而是一个信息性的消息。它表明在指定的路径`/Users/carrot/carrotFile/Knowledge/.git/`下初始化了一个空的Git仓库。这通常发生在执行`git init`命令时。


把文件添加到版本库中，使用命令 git add .添加到暂存区里面去，不要忘记后面的小数点“.”，意为添加文件夹下的所有文件
git add .

用命令 git commit告诉Git，把文件提交到仓库。引号内为提交说明
git commit -m '提交信息'

关联到远程仓库
 git remote add origin 你的远程库地址
 例：
```js
git remote add origin https://github.com/bodanli159951/angularJS-webApp.git
```

获取远程库与本地同步合并（如果远程库「不为空」则必须做这一步，否则后面的提交会失败）

```js
git pull --rebase origin master
```
 
把本地库的内容推送到远程，使用 git push命令，实际上是把当前分支master推送到远程。执行此命令后会要求输入用户名、密码，验证通过后即开始上传。
```js
git push -u origin master
```

状态查询命令
```js
git status
```


### 问题

remote: Support for password authentication was removed on August 13, 2021. Please use a persona
意思就是说，如果是你之前是密码登陆的，现在需要用token登陆；

生成token
首先，登陆github 网站，点击网页右上角头像，依次找到 `Setting` 和 `Develop Setting`

选择个人访问令牌Personal access tokens，然后选中生成令牌Generate new token

设置token的有效期，访问权限等
- 选择要授予此令牌token的范围或权限。
- 要使用token从命令行访问仓库，请选择repo
- 要使用token从命令行删除仓库，请选择delete_repo
- 其他根据需要进行勾选

把生成的token粘贴到输入密码的位置
也可以 把token直接添加远程仓库链接中
```js
git remote set-url origin https://<your_token>@github.com/<USERNAME>/<REPO>.git

git remote set-url origin https://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@github.com/shliang0603/Yolov4_DeepSocial.git/
```

Toekn: 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


### git 区域

工作区（working Directory）
定义：在本地计算机上实际操作的文件夹
作用：在工作区中，你可以自由地修改文件。所有的编辑、创建和删除操作都在这个区域进行
状态：文件的状态通常为以下几种
- **未跟踪（Untracked）**: 新添加的文件，尚未被 Git 跟踪。
- **已修改（Modified）**: 文件已被修改，但是还没有被暂存。
- **已跟踪（Tracked）**: Git 正在跟踪的文件，可以是未修改、已修改或已删除状态。

暂存区（）
定义：暂存区是一个中间区域，用于暂时保存即将提交到本地仓库的文件更改
作用：暂存区允许你选择性地准备将哪些更改包含在下一次提交中。这意味着，你可以通过添加和移除文件来控制提交的内容
操作
- 使用 `git add [file]` 可以将文件从工作区添加到暂存区。
- 使用 `git reset [file]` 可以将文件从暂存区移回到工作区（撤销暂存）。

本地仓库
定义：本地仓库是 Git 在你的计算机上保存所有历史版本的地方，通常包含 .git 目录。
作用：在本地仓库中，Git 存储所有的提交信息、版本历史和其他元数据。这是 Git 版本控制的核心。
操作：
提交更改：使用 git commit -m "message" 命令将暂存区的更改保存为一个新的提交。在这一操作之后，它们在本地仓库中创建一个新的版本。
查看提交历史：使用 git log 查看本地仓库中的提交记录。

三个区域的工作流程

在工作区中进行更改：编辑文件，添加文件或删除文件。
将更改添加到暂存区：通过 git add [file] 命令将想要提交的更改添加到暂存区。
提交更改：使用 git commit -m "message" 将暂存区的更改提交到本地仓库，同时创建一个新的提交记录。
重复以上步骤：继续在工作区中修改文件，添加到暂存区并提交，直到你完成所有的更改。


git 常用指令
git init 初始化一个新的 Git 仓库
git clone 从指定 URL 克隆一个远程仓库
git status 查看工作区和暂存区的状态，显示哪些文件已修改、哪些已暂存等
git add 文件名 将文件添加到暂存区
git commit -m '提交信息' 将暂存区的更改提交到本地仓库，并附上提交信息
git log 查看提交历史，显示每次提交的信息（SHA 值、作者、日期等）
git diff 查看尚未暂存的文件与最近一次提交之间的差异
git branch
git branch [branch-name]创建一个新分支
git checkout [branch-name]切换到指定的分支
git merge [branch-name] 将指定分支合并到当前分支

常见工作流
克隆仓库：git clone [url]
创建新分支：git checkout -b [new-branch]
修改文件，添加更改：git add [file]
提交更改：git commit -m "description"
切换回主分支：git checkout main
合并分支：git merge [new-branch]
推送更改到远程：git push origin main


[【Gitee版】一篇教你如何快速入门git(详解)\_git gitee-CSDN博客](https://blog.csdn.net/U2396573637/article/details/143063554)