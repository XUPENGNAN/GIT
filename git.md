##### Bash文件夹基本操作
1. cd : 改变目录
2. cd . .  : 回退到上一个目录，直接cd进入默认目录
3. pwd : 显示当前所在的目录路径
4. ls(ll): 都是列出当前目录中的所有文件，只不过ll(两个ll)列出的内容更为详细
5. touch : 新建一个文件
6. rm : 删除一个文件, rm index.js 就会把index.js文件删除
7. mkdir :新建一个文件夹
8. rm -r : 删除一个文件夹, rm -r src 删除src目录
9. mv : 移动文件 mv index.html src index.html 是我们要移动的文件, src 是目标文件夹,当然, 这样写,必须保证文件和目标文件夹在同一目录下
10. reset : 重新初始化终端/清屏
11. clear : 清屏
12. history : 查看命令历史
13. help : 帮助
14. exit : 退出
15. '#' : 注释

##### git 配置
1. git config -l ：查看所有配置项
2. git config --system --list ： 查看系统config
3. git config --global  --list ：查看当前用户（global全局）配置
4. git config --local  --list ： 查看当前仓库配置信息
5. 提交之前的配置标识，标识是谁提交的
   git config --global user.name "xxxxxxx"
 　git config --global user.email "xxxxxxx@qq.com"

6. 非全局配置：
   git config user.name "XXXXXXX"
   git config user.email "XXXXXXXX@qq.com"
                
7. 删除配置项:
  git config [--local || --global || --system] --unset section.key

##### git 工作区域划分
1. 工作区（本地新建的文件） ----git add(添加到)----->>  暂存区（.git目录下） ----git commit(提交到)------->>  本地仓库（.git目录下）

---- git push (提交到远程代码库) ---->>  远程代码库GitHub


2. 工作区（本地新建的文件） <<----git checkout(从本地仓库检出到工作区)-------  本地仓库（.git目录下）

<<----git clone (从远程代码库克隆到本地仓库)----  远程代码库GitHub


3. 工作区（本地新建的文件） <<----git pull (从远程代码库克隆到工作区)-----  远程代码库GitHub

##### git 提交的基本操作
1. 创建全新的仓库并提交到远程仓库（基本操作）
1.1 git init        # 在当前目录新建一个Git代码库
1.2 git add a.txt   # 提交指定文件  / git add . # 把该目录下的文件都提交
1.3 git commit -m '第一次提交'
1.3 在Github上设置好SSH密钥后，新建一个远程仓库，通过git remote add origin https://github.com/guyibang/TEST2.git                  将本地仓库和远程仓库进行关联
1.4 git push -u origin master   #提交到远程仓库

2. 设置本地的ssh key密匙
命令行输入：ssh-keygen -t rsa -C "XXXXXX@XXXX.com"       其中双引号中是你注册github时用的邮箱
会在默认路径下生成.ssh文件夹，打开.ssh里面有两个文件，打开id_rsa.pub复制里面的密钥
打开github,选择settings
点击new ssh key
将 id_rsa.pub 文件中的密匙复制进去

填坑：在mac下由于这个文件夹是隐藏的所用看不到，我们可以 

 ```
 cd ~/.ssh             //进入这个文件
 more id_rsa.pub       //显示这个文件的密匙内容
 ```

##### git 团队
1. leader上传代码到github:参考上一个
2. 保存代码的仓库 ---> settings ----> collaborator ----> 填写邀请者的 github 账号 -----> 进行邀请
------> 受邀者会在邮箱里收到邀请信息接受邀请 ----->leader可以看到同意的受邀者
3. 受邀者同样需要在本地创建密匙，与自己的 github 绑定 。
4. 受邀者将本地仓库和远程仓库进行关联，git remote add origin https://github.com/guyibang/TEST2.git        
5. 然后受邀者将代码克隆下来，git clone https://github.com/guyibang/TEST2.git 
6. 或者受邀者使用 git pull https://github.com/guyibang/TEST2.git 将代码复制下来
7. 多人同时操作一个文件时遇到冲突需要先进行，git pull , 然后再git push

##### git 创建本地分支
1. 创建本地分支 ： git branch 分支名
2. 切换分支 : git checkout 分支名
3. 查看当前分支 : git branch
[注：在dev分支上更改的文件或者内容在其他分支上不可见，只有切换到当前分支才可以看见]
4. 命令用于合并指定分支到当前分支 ： git merge dev
5. 删除分支： git branch -d dev

##### github 上创建分支
1. 仓库点击Branch，创建dev开发分支
2. 由于dev分支是从master分支上创建的，因此内容与master分支一致
[刚开始创建名为dev的分支时，如果master主分支上有内容那么dev分支将继承master主分支的内容]
3. 随后我们再往指定的github的分支上提交代码时，github主分支master将不会呈现其他分支上的内容。

##### 实际操作本地分支与github分支的操作
1. 项目中 github 一般会有 master 主分支，在这个分支上的代码一般为上线正式版本。
   在 github 上还会有一个 dev 分支，这里一般为开发版本的分支，其上的代码为开发时的代码。
   我们将开发的代码提交到 dev 分支上。

2. 本地也一般会创建一个主分支 master，一个属于你自己的 dev_mn 分支。
在 dev_mn 上自己的代码书写进行开发，然后将 dev_mn 合并到 本地master，(命令用于合并指定分支到当前分支 ： git merge dev)
再使用本地 master 主分支进行代码提交到 github 的dev 分支上
命令：git push origin master:dev

3. 在本地主分支 master上将远程github的dev上的代码pull下来：git checkout master ，git pull origin dev

4. 再切换到本地 dev_mn 上，使用命令：git rebase master ，在 dev_mn 上使用命令与从远程dev分支上 pull的在本地master上的代码进行比较。

5. 在本地 dev_mn 上反复执行命令，
git add .

git rebase --continue（继续解决冲突）
就会在本地的dev_mn上发现与远程pull下来的在本地master上的冲突，手动解决冲突，然后提交到远程
















 
