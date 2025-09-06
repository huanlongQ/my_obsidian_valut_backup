- [‎Gemini - CMD Git 入门指南](https://g.co/gemini/share/5270797f61b5)
- [Gemini - Git Line Endings and Filename Errors](https://g.co/gemini/share/3ac13b269887) 
* [Windows系统下设置cmd命令行(终端)走代理的方法 - zhuibo6 - 博客园](https://www.cnblogs.com/yerenwz/p/15925848.html) 
- [Gemini - Git 与 GitHub 仓库连接指南, 包括credentials manager, multi remote push](https://g.co/gemini/share/42fd27030128)
- [gemini - git lfs manual](https://g.co/gemini/share/9d663482bbbd) 

# Summary

## `config setting` 

```powershell
//alias
git config --global alias.co checkout
git config --global alias.br branch
git config --global alias.ci commit
git config --global alias.st status
git config --global alias.logl = log --oneline // better 

[log]
  date = relative
[format]
  pretty = format:%h %Cblue%ad%Creset %ae %Cgreen%s%Creset

//settings
git config --global init.defaultBranch main
git config --global http.proxy http://127.0.0.1:10809 //127.0.0.1:1080
git config --global https.proxy http://127.0.0.1:10809
git config --global --unset http.proxy
git config --global --unset https.proxy
git config --global core.longpaths true // give validity to long name files
```

## `checkout`

| 你的目的            | `git checkout` 命令                        | 现代替代命令                                        |
| --------------- | ---------------------------------------- | --------------------------------------------- |
| **切换到一个已存在的分支** | `git checkout <branch>`                  | `git switch <branch>`                         |
| **创建并切换到新分支**   | `git checkout -b <new-branch>`           | `git switch -c <new-branch>`                  |
| **临时查看某个旧版本**   | `git checkout <commit>`                  | `git switch --detach <commit>`                |
| **放弃对文件的本地修改**  | **`git checkout -- <file>`**             | `git restore <file>`                          |
| **从别处恢复单个文件**   | `git checkout <source_branch> -- <file>` | `git restore --source=<source_branch> <file>` |
| **解决合并冲突**      | `git checkout --ours/--theirs -- <file>` | (无直接替代，仍使用 `checkout`)                        |

| 功能                                                           | `git checkout` (旧)                          | `git switch` (新)           | `git restore` (新)                     | `git revert`             | `git rm --cached`        |
| ------------------------------------------------------------ | ------------------------------------------- | -------------------------- | ------------------------------------- | ------------------------ | ------------------------ |
| **切换分支**                                                     | `git checkout branch-name`                  | `git switch branch-name`   | 不适用                                   | 不适用                      |                          |
| **创建并切换分支**                                                  | `git checkout -b new-branch`                | `git switch -c new-branch` | 不适用                                   | 不适用                      |                          |
| **丢弃未暂存的修改**                                                 | `git checkout -- file.txt`                  | 不适用                        | `git restore file.txt`                | 不适用                      |                          |
| **将暂存区文件撤销**                                                 | **`git checkout HEAD -- file.txt`** $\star$ | 不适用                        | **`git restore --staged file.txt`** ⭐ | 不适用                      | `git rm --cached <file>` |
| **重新提交一个新的commit以覆盖掉不好的上一个commit, 新commit与前数两个版本的commit一致**. | 不适用                                         | 不适用                        | 不适用                                   | `git revert <commit_id>` |                          |

## `remote` 

- [Gemini - Git 与 GitHub 仓库连接指南, 包括credentials manager, multi remote push](https://g.co/gemini/share/42fd27030128)
- [‎Gemini - git lfs install and remote](https://g.co/gemini/share/f9d2a3ba9a26) 

| 命令            | 示例                                                                                                                                                                                         | 描述                                                                                                                                                                                 |
| ------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `git remote ` | 查看、添加或删除远程仓库的配置。`-v` 显示详细信息。<br>`git remote -v`<br>`git remote add origin <url>`<br>`git remote set-url --add origin https://github.com/你的用户名/仓库B.git`<br>`git remote remove origin <url>` | **git首次链接remote时会弹出GCM(Git Credential Manager), 绑定在Git上用于管理remote向各个remote repo的credentials.** <br>**`git push`同时给两个remote repo push内容, 使用`git remote set-url --add origin <url>** |
| `git fetch`   | `git fetch origin`                                                                                                                                                                         | 从远程仓库**获取**最新的历史记录，但**不合并**到你本地的分支。                                                                                                                                                |
| `git pull`    | `git pull origin main`<br>`git pull origin main --allow-unrelated-histories`                                                                                                               | 从远程仓库获取最新历史记录并**自动合并**到你当前的分支 (`fetch` + `merge`)。                                                                                                                                 |
| `git push`    | `git push origin main` <br>`git push -u origin local_main:remote_main`                                                                                                                     | 将本地分支的提交**推送**到远程仓库。`-u` 用于首次推送时建立本地与远程分支的关联。<br>`git push -u origin master`(`--set-upstream`)的作用是设置上游分支，这样之后你只需要简单地使用 `git push` 和 `git pull` 即可，Git 会知道要推送到哪个远程分支。               |

### `git lfs manual` 
![[Pasted image 20250906201302.png]]

![[Pasted image 20250906201138.png]]

![[Pasted image 20250906200947.png]]
- [gemini - git lfs manual](https://g.co/gemini/share/9d663482bbbd) 
**if error, remove remote and add them back, then push.**  
1) `git remote remove origin`
2) `git remote add origin <url_1>`
3) `git remote set-url --add origin <url_2>`

# `git` conceptions

- `commit`
- `branch` 
	- `HEAD`头指针 and `detached HEAD` by **`checkout`**  
	- 基于旧版本的新`commit`应该在一个新的`brach`里面, 而不是本`branch`的尾部. 
- `clone` $\to$ folder `orign/` 
- `git restore` or `git checkout` **do not use this cmd if not familiar i think.** 
	- **当某个文件已经被 Git 跟踪（之前 `add` 过），现在你在工作区又改动了它，但还没 `add`，想让这个文件回到上一次提交（或上一次 `add`）的状态**
	- **当你已经 `git add <file>` 把文件放进了暂存区（Index），但发现不该提交，想把它“撤下来”，让它回到工作区（状态回到修改后、未暂存）**
- `diffdecoration`
	- VScode extension git graph and **`diff decoration`**. 
	- `git diff id1 di2` 

# `git` cmd tutorial 

好的，很乐意教你如何在 Windows 的命令提示符（CMD）中使用 Git。Git 是一个非常强大的版本控制工具，可以帮助你管理代码、跟踪文件变更以及与他人协作。

下面我将从安装、配置到常用操作，一步步为你讲解。

### 1. 安装 Git

首先，你的电脑上需要安装 Git。

- **下载地址**：访问 Git 官方网站 [https://git-scm.com/download/win](https://git-scm.com/download/win) 下载适用于 Windows 的安装程序。
    
- **安装过程**：
    
    - 下载后，双击 `.exe` 文件开始安装。
        
    - 在安装过程中，你可以一直点击 "Next" 使用默认设置。这些默认选项对于初学者来说是完全足够且推荐的。
        
    - 安装程序会自动将 Git 添加到系统的环境变量中，这样你就可以在 CMD 中直接使用 `git` 命令了。
        
- **验证安装**： 安装完成后，打开命令提示符（CMD）。你可以通过在开始菜单搜索 "cmd" 或按 `Win + R` 键输入 `cmd` 并回车来打开。 在 CMD 中输入以下命令并回车：

    ```
    git --version
    ```
    
    如果安装成功，它会显示你安装的 Git 版本号，例如 `git version 2.45.1.windows.1`。

### 2. 初次使用 Git 前的配置

在使用 Git 之前，你需要设置你的用户名和电子邮件地址。这样，你在提交代码时，Git 就能记录是谁做的更改。

在 CMD 中依次输入以下命令，并替换成你自己的信息：

```
git config --global user.name "Your Name"
git config --global user.email "youremail@example.com"
```

- `--global` 参数表示这台电脑上所有的 Git 仓库都会使用这个配置。

你可以使用下面的命令来检查你的配置信息：

```
git config --list
```

### 3. Git 核心概念

在开始使用命令之前，理解几个核心概念很重要：

- **仓库 (Repository / Repo)**：你的项目文件夹，Git 在这里跟踪所有文件的变更。它可以是本地的，也可以是远程的（比如在 GitHub 或 Gitee 上）。
    
- **工作区 (Working Directory)**：你电脑上能看到的项目文件夹，包含了项目的实际文件。
    
- **暂存区 (Staging Area / Index)**：一个临时的区域，用于存放你希望在下一次“提交”中记录的变更。你可以把文件的修改、新增等先 “添加” 到这里。
    
- **本地仓库 (Local Repository)**：Git 在你的电脑上存储项目历史记录的地方。当你“提交”后，暂存区的变更就会被永久记录到本地仓库中。
    
- **远程仓库 (Remote Repository)**：托管在网络服务器上的项目仓库（例如 GitHub），方便你和团队成员协作和共享代码。

**基本流程**： 在 **工作区** 修改文件 -> 将修改过的文件 **添加到暂存区** -> 将暂存区的文件 **提交到本地仓库** -> （可选）将本地仓库的提交 **推送到远程仓库**。

### 4. CMD 中常用的 Git 命令

下面我们通过一个实际的例子来学习最常用的命令。

#### **步骤一：创建或进入项目文件夹**

首先，你需要有一个项目文件夹。我们先在 D 盘创建一个名为 `my-project` 的文件夹作为示例。

```
D:
mkdir my-project
cd my-project
```

- `D:` 切换到 D 盘。
    
- `mkdir my-project` 创建一个名为 `my-project` 的文件夹。
    
- `cd my-project` 进入这个文件夹。

#### **步骤二：初始化一个新的 Git 仓库**

在这个文件夹里，使用 `git init` 命令来创建一个新的本地 Git 仓库。

```
git init
```

执行后，你会看到提示 `Initialized empty Git repository in D:/my-project/.git/`。这会在你的项目文件夹里创建一个隐藏的 `.git` 文件夹，所有版本控制相关的信息都存储在这里。

#### **步骤三：查看仓库状态**

`git status` 是你最常用的命令之一，它可以告诉你当前仓库的状态。

```
git status
```

由于我们刚初始化，还没有任何文件，它会提示 `No commits yet` 和 `nothing to commit`。

#### **步骤四：创建文件并添加到暂存区**

现在，我们在项目里创建一个文件。

1. 创建一个 `readme.txt` 文件，并写入一些内容。你可以手动创建，也可以用命令：

    ```
    echo "Hello, Git!" > readme.txt
    ```
    
2. 再次使用 `git status` 查看状态。你会看到 `readme.txt` 文件被列为 "Untracked files"（未跟踪的文件）。
    
3. 使用 `git add` 命令将这个文件添加到暂存区，让 Git 开始跟踪它。

    ```
    git add readme.txt
    ```
    
    - 如果你想添加所有修改过的文件，可以使用 `git add .`
        
4. 再次使用 `git status`，你会看到 `readme.txt` 现在被列在 "Changes to be committed"（待提交的更改）下面了。

#### **步骤五：提交更改到本地仓库**

文件进入暂存区后，就可以使用 `git commit` 将这些更改永久记录到本地仓库了。

```
git commit -m "Add initial readme file"
```

- `-m` 参数后面跟着的是本次提交的说明信息，这个信息非常重要，应该清晰地描述你这次提交做了什么改动。

提交后，再次使用 `git status`，它会告诉你 `nothing to commit, working tree clean`，表示工作区和本地仓库已经同步。

#### **步骤六：查看提交历史**

你可以使用 `git log` 来查看所有的提交记录。

```
git log
```

它会列出每次提交的哈希值（一个唯一的ID）、作者、日期和提交说明。

---

### 5. 与远程仓库协作 (以 GitHub 为例)

通常，你会把代码托管到像 GitHub 这样的平台上，方便备份和团队协作。

#### **步骤一：创建远程仓库**

在 GitHub 网站上创建一个新的空仓库，比如也叫 `my-project`。创建后，不要勾选任何 "Initialize this repository with..." 的选项。GitHub 会给你一个仓库地址，比如 `https://github.com/your-username/my-project.git`。

#### **步骤二：关联远程仓库**

回到 CMD，在你的本地项目文件夹中，使用 `git remote add` 命令将本地仓库与远程仓库关联起来。

```
git remote add origin https://github.com/your-username/my-project.git
```

- `origin` 是远程仓库的默认别名。

#### **步骤三：推送本地提交到远程仓库**

使用 `git push` 命令将本地的提交推送到远程仓库。

```
git push -u origin master
```

或者，如果你的默认分支是 `main`（现在 GitHub 新建仓库默认为 `main`）：

```
git push -u origin main
```

- `-u` 参数会将本地的 `master` (或 `main`) 分支与远程的 `origin/master` (或 `origin/main`) 分支关联起来。这样，以后你再推送时，只需要输入 `git push` 就可以了。

#### **步骤四：从远程仓库拉取/克隆**

- **克隆仓库**：如果你想把一个远程仓库完整地下载到本地（比如参与一个已有项目），你应该使用 `git clone`。

    ```
    git clone https://github.com/someone-else/another-project.git
    ```
    
    这会自动创建一个 `another-project` 文件夹，并把所有代码和历史记录都下载下来。
    
- **拉取更新**：如果你的同事向远程仓库推送了新的提交，你需要使用 `git pull` 来获取这些更新，并与你的本地代码合并。

    ```
    git pull origin main
    ```

### 常用命令总结

| 命令                             | 功能                      |
| ------------------------------ | ----------------------- |
| `git init`                     | 初始化一个新的本地仓库。            |
| `git status`                   | 查看当前仓库的状态（哪些文件被修改、暂存等）。 |
| `git add <file>` 或 `git add .` | 将文件的修改添加到暂存区。           |
| `git commit -m "message"`      | 将暂存区的内容提交到本地仓库，并附上说明。   |
| `git log`                      | 查看提交历史记录。               |
| `git clone <url>`              | 从远程仓库下载一个完整的项目副本。       |
| `git remote add origin <url>`  | 关联一个远程仓库。               |
| `git push`                     | 将本地的提交推送到远程仓库。          |
| `git pull`                     | 从远程仓库获取最新的更改并合并到本地。     |
| `git branch`                   | 查看、创建或删除分支。             |
| `git checkout <branch>`        | 切换到指定分支。                |
| `git merge <branch>`           | 将一个分支的更改合并到当前分支。        |
|                                |                         |

# `git config settings` 

* [Windows系统下设置cmd命令行(终端)走代理的方法 - zhuibo6 - 博客园](https://www.cnblogs.com/yerenwz/p/15925848.html) 
*  [Gemini - Git Line Endings and Filename Errors](https://g.co/gemini/share/3ac13b269887)

```powershell
//alias
git config --global alias.co checkout
git config --global alias.br branch
git config --global alias.ci commit
git config --global alias.st status
git config --global alias.logl = log --oneline

[log]
  date = relative
[format]
  pretty = format:%h %Cblue%ad%Creset %ae %Cgreen%s%Creset

//settings
git config --global init.defaultBranch main
git config --global http.proxy http://127.0.0.1:10809 //127.0.0.1:1080
git config --global https.proxy http://127.0.0.1:10809
git config --global --unset http.proxy
git config --global --unset https.proxy
git config --global core.longpaths true // give validity to long name files
```

# `git` version control 

- `git checkout commitID`

### Git 常用命令大全 (按功能分类)

#### 1. 设置与初始化 (Setup & Initialization)

|命令|示例|描述|
|---|---|---|
|`git config`|`git config --global user.name "Your Name"`|设置 Git 的配置信息（用户名、邮箱、别名等）。`--global` 表示全局配置。|
|`git init`|`git init`|在当前目录初始化一个新的 Git 仓库。|
|`git clone`|`git clone <repository_url>`|从远程地址克隆一个完整的仓库到本地。|

---

#### 2. 日常核心操作 (Core Daily Workflow)

| 命令           | 示例                                    | 描述                                               |
| ------------ | ------------------------------------- | ------------------------------------------------ |
| `git status` | `git status`                          | 查看工作区和暂存区的状态，这是最最常用的命令。                          |
| `git add`    | `git add <file>` 或 `git add .`        | 将文件的修改添加到暂存区（Staging Area）。`.` 代表所有更改。           |
| `git commit` | `git commit -m "Your commit message"` | 将暂存区的内容提交到本地仓库，形成一个新的版本快照。                       |
| `git log`    | `git log --oneline --graph`           | 查看提交历史记录。`--oneline` 以简洁的一行显示，`--graph` 显示分支合并图。 |

---

#### 3. **分支管理 (Branching)**

这是 Git 的精髓所在。`checkout` 是老命令，功能复杂；`switch` 和 `restore` 是新命令，功能专一，推荐使用。

| 命令                    | 示例                                                                             | 描述                                            |
| --------------------- | ------------------------------------------------------------------------------ | --------------------------------------------- |
| `git branch`          | `git branch` <br> `git branch <new_branch>` <br> `git branch -d <branch_name>` | 列出、创建或删除分支。`-d` 用于删除已合并的分支, `-D` 强制删除。        |
| **`git switch` (推荐)** | `git switch <branch_name>` <br> `git switch -c <new_branch>`                   | **切换分支**。`-c` (create) 表示创建并切换到新分支。           |
| `git checkout` (旧命令)  | `git checkout <branch_name>` <br> `git checkout -b <new_branch>`               | 切换分支。`-b` (branch) 表示创建并切换到新分支。它功能太多，还用于恢复文件。 |
| `git merge`           | `git merge <branch_to_merge>`                                                  | 将指定分支的更改合并到**当前所在的分支**。                       |

---

#### 4. 撤销与恢复 (Undoing & Restoring)

- `git restore` or `git checkout`
	- **当某个文件已经被 Git 跟踪（之前 `add` 过），现在你在工作区又改动了它，但还没 `add`，想让这个文件回到上一次提交（或上一次 `add`）的状态**
	- **当你已经 `git add <file>` 把文件放进了暂存区（Index），但发现不该提交，想把它“撤下来”，让它回到工作区（状态回到修改后、未暂存）**

| 命令                     | 示例                                                      | 描述                                                  |
| ---------------------- | ------------------------------------------------------- | --------------------------------------------------- |
| **`git restore` (推荐)** | `git restore <file>` <br> `git restore --staged <file>` | **撤销工作区的修改**或**将文件从暂存区移回工作区**。这是 `checkout` 的另一半功能。 |
| `git checkout` (旧命令)   | `git checkout -- <file>`                                | 撤销对工作区某个文件的修改（危险，因为不进回收站）。                          |
| `git reset`            | `git reset --hard <commit_id>`                          | **回退版本**，移动 `HEAD` 指针。会改写历史，主要用于本地仓库。               |
| **`git revert`** <br>⭐ | `git revert <commit_id>`                                | **创建一个新的提交来撤销**某个旧提交。不会改写历史，安全，适用于远程仓库。             |
| `git clean`            | `git clean -n` <br> `git clean -f`                      | 从工作区中删除未被 Git 跟踪的文件。`-n` 预览将删除的文件, `-f` 强制删除。       |

---

#### 5. 远程仓库协作 (Remote Repositories)

| 命令                                                                                                   | 示例                                                                           | 描述                                                                                                                                                                   |
| ---------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `git remot `<br>`git remote -v`<br>`git remote add origin <url>`<br>`git remote remove origin <url>` | 查看、添加或删除远程仓库的配置。`-v` 显示详细信息。                                                 |                                                                                                                                                                      |
| `git fetch`                                                                                          | `git fetch origin`                                                           | 从远程仓库**获取**最新的历史记录，但**不合并**到你本地的分支。                                                                                                                                  |
| `git pull`                                                                                           | `git pull origin main`<br>`git pull origin main --allow-unrelated-histories` | 从远程仓库获取最新历史记录并**自动合并**到你当前的分支 (`fetch` + `merge`)。                                                                                                                   |
| `git push`                                                                                           | `git push origin main` <br>`git push -u origin local_main:remote_main`       | 将本地分支的提交**推送**到远程仓库。`-u` 用于首次推送时建立本地与远程分支的关联。<br>`git push -u origin master`(`--set-upstream`)的作用是设置上游分支，这样之后你只需要简单地使用 `git push` 和 `git pull` 即可，Git 会知道要推送到哪个远程分支。 |

---

#### 6. 高级与实用工具 (Advanced & Useful Tools)

| 命令                | 示例                                                                      | 描述                                                       |
| ----------------- | ----------------------------------------------------------------------- | -------------------------------------------------------- |
| `git diff`        | `git diff` <br> `git diff --staged` <br> `git diff <commit1> <commit2>` | 查看文件内容的差异。默认为工作区与暂存区的差异；`--staged` 为暂存区与上次提交的差异。         |
| `git stash`       | `git stash` <br> `git stash pop`                                        | 将当前工作区和暂存区的修改临时“储藏”起来，让工作区变干净。`pop` 用于恢复。                |
| `git tag`         | `git tag -a v1.0 -m "Version 1.0"`                                      | 为某个重要的提交打上标签，通常用于标记发布版本。                                 |
| `git rebase`      | `git rebase <base_branch>`                                              | “变基”操作。将当前分支的提交“重新播放”在目标分支之上，可以获得线性的提交历史。**不要在公共分支上使用**。 |
| `git cherry-pick` | `git cherry-pick <commit_id>`                                           | “捡樱桃”。将某个分支的**单个提交**复制到当前分支上。                            |

### `checkout` vs `switch`/`restore` 总结

为了让你更好地理解为什么要用新命令，请看下表：

| 你想做什么？       | 旧命令 (`checkout`)                | 新命令 (推荐)                    |
| ------------ | ------------------------------- | --------------------------- |
| **切换分支**     | `git checkout my-feature`       | `git switch my-feature`     |
| **创建并切换分支**  | `git checkout -b new-feature`   | `git switch -c new-feature` |
| **撤销工作区的修改** | `git checkout -- some-file.txt` | `git restore some-file.txt` |

你看，新命令 `switch` 只负责分支切换，`restore` 只负责文件恢复，职责单一，不容易误用。

**学习建议：** 你不需要一次性记住所有命令。先把“日常核心操作”和“分支管理”中的 `branch`、`switch`、`merge` 弄明白，就已经能应对 80% 的工作场景了。遇到具体问题时，再来查阅这份列表。

你也可以随时在 CMD 中使用 `git --help` 或者 `git <command> --help` 来查看任何命令的详细用法。

# `git checkout`

### 第一大功能：切换指针 (`HEAD`)

这是 `checkout` 最核心的功能，即移动 `HEAD` 指针，决定你当前工作的上下文。这可以是在不同的分支（时间线）之间切换，也可以是切换到历史上的某个具体时间点。

- #### 场景A：切换分支 (最常用)
    
    这是在不同的开发故事线之间跳转。

    ```
    # 从当前分支切换到 'develop' 分支
    git checkout develop
    ```
    
- #### 场景B：创建并切换分支
    
    这是“创建分支”和“切换分支”两个动作的合并，非常高效。

    ```
    # 基于当前位置，创建一个名为 'new-feature' 的新分支，并立刻切换过去
    git checkout -b new-feature
    ```
    
- #### 场景C：切换到特定提交 (进入“游客模式”)
    
    这是回到过去某个精确的时间点进行查看或测试，会导致“分离头指针”(Detached HEAD)状态。

    ```
    # 切换到 commit id 为 a8b4b8e 的历史状态
    git checkout a8b4b8e
    ```

> **⭐ 现代替代方案 (`git switch`)**
> 
> Git 2.23 版本之后，官方推荐使用 `git switch` 来专门处理以上所有场景，因为它的名字更能体现“切换分支”这个意图。
> 
> - `git switch develop`
>     
> - `git switch -c new-feature`
>     
> - `git switch --detach a8b4b8e` (切换到 commit)
>     

---

### 第二大功能：恢复工作区的文件

这个功能**不移动 `HEAD` 指针**，也就是说，你还停留在当前的分支和 commit 上。它的操作对象是工作区里的具体文件，用来撤销修改。

- #### 场景A：放弃对文件的本地修改
    
    将某个文件恢复到它在暂存区或上一次 commit 时的状态，**会删除所有未保存的本地修改**。

    ```
    # 撤销对 'config.yml' 的所有修改
    git checkout -- config.yml
    ```
    
    _(注意 `--` 是一个好习惯，用来明确告诉 Git 后面的是文件名，而不是分支名)_
    
- #### 场景B：从别的分支或过去的某个提交中“捞”一个文件过来
    
    这是一个非常强大的功能，可以让你在不切换整个项目的情况下，只把某一个文件的特定版本取过来。

    ```
    # 将 'main' 分支的 'main.py' 文件内容，覆盖到我当前的分支中
    git checkout main -- main.py
    
    # 从过去的 commit a8b4b8e 中，只把 'utils.py' 这一个文件恢复出来
    git checkout a8b4b8e -- utils.py
    ```

> **⭐ 现代替代方案 (`git restore`)**
> 
> 同样，官方推荐使用 `git restore` 来专门处理文件恢复，意图更清晰。
> 
> - `git restore config.yml` (放弃本地修改)
>     
> - `git restore --source=main main.py` (从其他地方“捞”文件)
>     

---

### 第三大功能：解决合并冲突 (特殊用途)

这是一个比较特殊的场景，只在 `git merge` 发生冲突时使用。`checkout` 可以帮你快速选择使用哪个版本的文件来解决冲突。

- #### 场景：合并 `feature` 分支到 `main` 时，`app.js` 文件冲突了

    ```
    # 选择使用我们自己的版本（即合并前 main 分支上的版本）
    git checkout --ours -- app.js
    
    # 选择使用他们的版本（即来自 feature 分支上的版本）
    git checkout --theirs -- app.js
    ```
    
    选择一个版本后，还需要 `git add app.js` 和 `git commit` 来完成合并。

---

### 总结表

| 你的目的            | `git checkout` 命令                        | 现代替代命令                                        |
| --------------- | ---------------------------------------- | --------------------------------------------- |
| **切换到一个已存在的分支** | `git checkout <branch>`                  | `git switch <branch>`                         |
| **创建并切换到新分支**   | `git checkout -b <new-branch>`           | `git switch -c <new-branch>`                  |
| **临时查看某个旧版本**   | `git checkout <commit>`                  | `git switch --detach <commit>`                |
| **放弃对文件的本地修改**  | **`git checkout -- <file>`**             | `git restore <file>`                          |
| **从别处恢复单个文件**   | `git checkout <source_branch> -- <file>` | `git restore --source=<source_branch> <file>` |
| **解决合并冲突**      | `git checkout --ours/--theirs -- <file>` | (无直接替代，仍使用 `checkout`)                        |

| 功能                                                           | `git checkout` (旧)                          | `git switch` (新)           | `git restore` (新)                     | `git revert`             | `git rm --cached`        |
| ------------------------------------------------------------ | ------------------------------------------- | -------------------------- | ------------------------------------- | ------------------------ | ------------------------ |
| **切换分支**                                                     | `git checkout branch-name`                  | `git switch branch-name`   | 不适用                                   | 不适用                      |                          |
| **创建并切换分支**                                                  | `git checkout -b new-branch`                | `git switch -c new-branch` | 不适用                                   | 不适用                      |                          |
| **丢弃未暂存的修改**                                                 | `git checkout -- file.txt`                  | 不适用                        | `git restore file.txt`                | 不适用                      |                          |
| **将暂存区文件撤销**                                                 | **`git checkout HEAD -- file.txt`** $\star$ | 不适用                        | **`git restore --staged file.txt`** ⭐ | 不适用                      | `git rm --cached <file>` |
| **重新提交一个新的commit以覆盖掉不好的上一个commit, 新commit与前数两个版本的commit一致**. | 不适用                                         | 不适用                        | 不适用                                   | `git revert <commit_id>` |                          |

# `git` and GitHub 

- [Gemini - Git 与 GitHub 仓库连接指南, 包括credentials manager, multi remote push](https://g.co/gemini/share/42fd27030128)

| 命令            | 示例                                                                                                                                                                                         | 描述                                                                                                                                                                                 |
| ------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `git remote ` | 查看、添加或删除远程仓库的配置。`-v` 显示详细信息。<br>`git remote -v`<br>`git remote add origin <url>`<br>`git remote set-url --add origin https://github.com/你的用户名/仓库B.git`<br>`git remote remove origin <url>` | **git首次链接remote时会弹出GCM(Git Credential Manager), 绑定在Git上用于管理remote向各个remote repo的credentials.** <br>**`git push`同时给两个remote repo push内容, 使用`git remote ser-url --add origin <url>** |
| `git fetch`   | `git fetch origin`                                                                                                                                                                         | 从远程仓库**获取**最新的历史记录，但**不合并**到你本地的分支。                                                                                                                                                |
| `git pull`    | `git pull origin main`<br>`git pull origin main --allow-unrelated-histories`                                                                                                               | 从远程仓库获取最新历史记录并**自动合并**到你当前的分支 (`fetch` + `merge`)。                                                                                                                                 |
| `git push`    | `git push origin main` <br>`git push -u origin local_main:remote_main`                                                                                                                     | 将本地分支的提交**推送**到远程仓库。`-u` 用于首次推送时建立本地与远程分支的关联。<br>`git push -u origin master`(`--set-upstream`)的作用是设置上游分支，这样之后你只需要简单地使用 `git push` 和 `git pull` 即可，Git 会知道要推送到哪个远程分支。               |
