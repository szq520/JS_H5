

## 关联 github 仓库
---

> 第一步，`先关联git仓库`

```bash
git clone https://github.com/guthub用户名/demo.git
```

> 第二步，`查看当前仓库的状态 (可选)`

```bash
git status
```

> 第三步，`把文件添加到暂存区`

```bash
# 单独添加一个文件或文件夹
git add demo.txt

# 添加多个文件或文件夹
git add demo1.txt demo2.txt

# 添加所有文件
git add --all
```

> 第四步，`把文件从暂存区提交到仓库`

```bash
git commit -m "本次提交说明"
```

> 第五步，`同步到github仓库`

```bash
git push
```

!> 如果是二次提交, 可以把第三步和第四步合并为 `git commit -a -m "本次提交说明"`

<br><br><br>

## 修改commit注释

```bash
# 重新修改上一次commit的注释
git commit --amend -m "新的描述信息"
```

<br><br><br>

## 版本回退

> 第一步，`先查看当前历史版本`

```bash
// 查看详细的版本信息
git log

// 查看简略的版本信息
git log --oneline
```

> 第二步，`回退到指定版本`

```bash
# 回退到上一个版本
git reset --hard HEAD^1

# 回退到上上一个版本
git reset --hard HEAD~2

# 回退到指定的版本号
git reset --hard 版本号
```

<br><br><br>

## 删除文件并恢复

```bash
# 删除本地文件，但版本库中还存在
rm 文件名
# git checkout是版本库替换工作区
git checkout -- 文件名
```

```bash
# 连同版本库中的文件一起删除删除
git rm 文件名
# 从上一个版本中单独把文件拎出来
git checkout HEAD -- 文件名
```

<br><br><br>