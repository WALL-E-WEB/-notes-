![git回顾](../image/git回顾.png)

# git

是版本管理软件

版本管理

### git init

```js
作用：初始化git仓库，想要使用git对某个项目进行管理，需要`git init`进行初始化
```

### git add .

```js
# 将index.html添加到暂存区
git add index.html

# 将css目录下所有的文件添加到暂存区
git add css

# 将当前目录下所有的js文件添加到暂存区
git add *.js

# 添加当前目录下所有的文件
git add .
git add -A
git add --all

注意点：空的文件夹是会被忽略掉的，如果想要提交这个文件夹，一般会在该目录下创建一个.gitkeep文件
```

### git status 

```js
查看提交状态
- 红色表示工作区中的文件需要提交
- 绿色表示暂存区中的文件需要提交
```



### git commit 

```js
# 将文件从暂存区提交到仓库
git commit -m "提交说明"

# 如果不写提交说明，会进入vi编辑器，没有写提交说明，是提交不成功的。
git commit   # 需要使用vi输入内容

# 如果是一个已经暂存过的文件，可以快速提交，如果是未追踪的文件，那么命令将不生效。
git commit -a -m '提交说明'

# 修改最近的一次提交说明， 如果提交说明不小心输错了，可以使用这个命令
git commit --amend -m "提交说明"
```

### git log

```js
- 作用：查看提交日志
git log查看提交的日志 
git log --oneline   
git reflog 查看全部
```

![git01](../image/git01.png)

### git diff

```js
# 查看工作区与暂存区的不同
git diff

# 查看暂存区与仓库区的不同
git diff --cached

# 查看工作区与仓库区的不同，HEAD表示最新的那次提交
git diff HEAD

# 查看两个版本之间的不同
git diff c265262 de4845b

# 查看pull下来的和上一次提交的差别
git diff HEAD^1

# 比当前提交新2个的提交的比较：
git diff HEAD~2
```

![git02](../image/git02.png)

### git reset

```js
作用：版本回退，将代码恢复到已经提交的某一个版本中。

git reset --hard 版本号

git reset --hard head~1`将版本回退到上一次提交
- ~1:上一次提交
- ~2:上上次提交
- ~0:当前提交

git reflog 查看所有版本信息
```

### git忽视文件

```js
在仓库的根目录创建一个`.gitignore`的文件，文件名是固定的。

将不需要被git管理的文件路径添加到`.gitignore`中.
# 忽视idea.txt文件
idea.txt

# 忽视css下的index.js文件
css/index.js

# 忽视css下的所有的js文件
css/*.js

# 忽视css下的所有文件
css/*.*
# 忽视css文件夹
css
```

### git pull

```js
拉 同步最新代码
```

### git 忽略文件

```js
1. touch .gitignore，生成.gitignore文件
2. 在生成的.gitignore文件里输入你要忽略

如:
node_modules/
dist/

配置规则：

以斜杠“/”开头表示目录；
以星号“*”通配多个字符；
以问号“?”通配单个字符；
以方括号“[]”包含单个字符的匹配列表；
以叹号“!”表示不忽略(跟踪)匹配到的文件或目录；

 配置文件是按行从上到下进行规则匹配的，意味着如果前面的规则匹配的范围更大
```



### 查看设置邮箱和用户

```js
	git config user.email
	git config user.name

##### 修改用户邮箱和用户名:

第一种办法:  直接重新再设置一下,他就会覆盖.

git config --global user.email "you@example.com"
git config --global user.name "Your Name" 

第二种办法:  退出再登录

	退出:
git  config  --global   --unset  user.email
git  config  --global   --unset  user.name
推荐大家使用 github注册的邮箱和用户名来登录.
```

### git branch

```js
新建分支: git branch 分支名
切换分支: git checkout 分支名
合并分支: git merge 分支名 //回到主分支合并
删除分支: git branch -d 分支名
```

## git stash -u 存档

```
git stash -u 存档
git stash pop

```



### 本地同步至githab

```js
git remote rm origin  //清除

git remote add origin https://

git push -u origin master
# 给远程仓库设置一个别名
git remote add 仓库别名 仓库地址
git remote add autumnFish git@github.com:autumnFish/test.git

# autumnFish
git remote remove autumnFish

# git clone的仓库默认有一个origin的别名


修改远程仓库地址
git remote set-url origin [url]
git push origin master
```

### git clone

```js
git clone https://

git push 
```

### git commit 常用

```js
feat： 新增 feature
fix: 修复 bug
docs: 仅仅修改了文档，比如 README, CHANGELOG, CONTRIBUTE等等
style: 仅仅修改了空格、格式缩进、逗号等等，不改变代码逻辑
refactor: 代码重构，没有加新功能或者修复 bug
perf: 优化相关，比如提升性能、体验
test: 测试用例，包括单元测试、集成测试等
chore: 改变构建流程、或者增加依赖库、工具等
revert: 回滚到上一个版本

updata
delete
add
fix
perf

```

廖雪峰讲git:

https://www.liaoxuefeng.com/wiki/896043488029600/896067008724000





https://www.liaoxuefeng.com/wiki/1022910821149312





http://www.ruanyifeng.com/blog/2015/07/flex-examples.html





http://es6.ruanyifeng.com/

​    



