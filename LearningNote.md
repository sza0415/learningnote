`gcc` 在编译 `source_filename.cpp` 时会产生中间目标文件，并且 `-lstdc++` 用于链接 C++ 标准库。最后，`-o output_filename` 部分将这些中间目标文件链接在一起生成最终的可执行文件 `output_filename`。s 优势、亮点、基本情况
 1.言简意赅、语言精炼，控制时间
 2.和应聘岗位相关的经历
 3.为什么能够胜任这个岗位
 4.为什么要应聘该岗位~求职动机

 注意：

重点介绍满足岗位要求的三个优势和亮点
 表现出对岗位的理解和自己清晰的职业规划
 表示愿意长期从事这个岗位

面试官您好，我叫xxx，来自浙江理工大学计算机科学与技术学院，很荣幸能够参加此次面试，今天我应聘的岗位是您公司的网络平台后端开发实习生-系统架构岗位。我曾在电力智能保障系统项目中对模型搭建、模型部署、模型的精度和推理性能的优化、以及多路视频流的处理进行实践。此外我结合岗位的要求进行了准备，<u>包括对计算机网络协议的熟悉</u>，常用算法的理解。我希望能够加入公司从事实际应用场景的工作，我的自我介绍到此结束，谢谢。

### Github工作流

- 假设我们在`github`上有一个仓库`repository` （可能是你自己的也可能是别人的），这个`repository`的主分支`branch`是`main`（原来叫`master`），我们假设这个`main`branch上面只有一个commit是`init` （实际上有若干个也无所谓）。现在我们管这个所有人都共享的`远端代码仓库`，也就是`github`叫做`remote`。![image-20231117151439605](C:\Users\91077\AppData\Roaming\Typora\typora-user-images\image-20231117151439605.png)

- 当我们想要修改或者贡献代码的时候，第一件事就是要把`remote`的仓库代码复制到本地，我们可以通过`git clone`命令在本地复制一个一模一样的仓库。

  ```bash
  git clone https://github.com/xxxx.git
  ```

  通常使用`git clone`克隆远程仓库的时候，Git会默认将远程仓库设置一个别名，比如`origin`，指向` https://github.com/xxxx.git`这个地址，后续关于远程仓库的操作可以查看==git remote==。

  这里注意我们最好要将本地看作为两个部分，一个叫做`local git`可以认为是本地的git 仓库（这里拥有所有你告诉git的信息），另一个叫做`disk`（也就是磁盘，这个部分是我们的源文件真正在磁盘里的样子，==这个后续会有解释==）。在我们刚进行完`git clone`操作后，`remote` 、`local`、`dist`都是一样的。

- ![image-20231117151938818](C:\Users\91077\AppData\Roaming\Typora\typora-user-images\image-20231117151938818.png)

- 在我们修改代码的时候，第一件事情就是建立一个新的`feature branch`（功能分支），而不是直接往`main`分支上面`push`代码，这样有很多好处：

  - 比如它不会把你的`main`主分支搞得不能工作
  - 此外它非常利于多人合作

  ![image-20231117154918602](C:\Users\91077\AppData\Roaming\Typora\typora-user-images\image-20231117154918602.png)

  建立自己的`feature branch`的方法就是使用`git checkout -b my-feature`（这个my-feature就是你设定`feature branch`功能分支的名称，当然由于`checkout`的语义太多，后续官方对`checkout`语义进行了拆分成了`branch`和`switch`）

  ```bash
  git checkout -b my-feature
  # 这个命令会复制一份你当前的branch（比如main）到你的新branch（即你的my-feature）上，并且切换到了新branch 上。
  ```

  通过`git checkout -b my-feature`命令，我们本地的`local git`本地仓库里有`main`分支和`my-feature` branch，这两个branch内容是一样的。

  当你使用`checkout`命令之后，`git`会将这个branch上面的源文件同步给硬盘`disk`，也就是硬盘`dist`里的代码就是这个branch里面的代码。举例：

  - 你可以使用`Git bash`到你`git clone`到本地的磁盘的文件下。![image-20231117155151248](C:\Users\91077\AppData\Roaming\Typora\typora-user-images\image-20231117155151248.png)

    你使用`git checkout -b my-feature`命令后![image-20231117155349688](C:\Users\91077\AppData\Roaming\Typora\typora-user-images\image-20231117155349688.png)

    此时你转移到了`my-feature`下，但是`disk`并没有发生变化（因为你是复制过来的，==后面若各个分支里内容不同，你再使用 git checkout 切换分支后，disk会显示该分支下的内容==）。

- 接下来我们可以修改代码了，不管是修bug还是加feature，当你改好代码保存文件后，你的硬盘上面的文件是有变化的，但是你的`Local git`对此一无所知。这个时候你可以使用`git diff`命令来看我现在这个硬盘上的这个改变跟我`Local git`保存的分支有什么区别。![image-20231117162740675](C:\Users\91077\AppData\Roaming\Typora\typora-user-images\image-20231117162740675.png)

  当我们确定要把修改的文件告知`local git`的时候，可以使用`git add <changed_file>`命令，你可以告诉`local git`所有你所修改的文件。`git add`命令会将这些文件放到一个==暂存区（具体内容可以去看后面的git工作流程）==的地方，当你使用`git add`添加完所有你想修改的文件之后，可以使用`git commit`来把这些真正的修改放到`local git`本地仓库当中，此时`local git`中将这些修改作为一个新的`commit`进行添加，可以看到`my-feature`分支中除了一开始的`init`commit，增加了一个新的commit。你可以通过命令`git commit -m 'xxx'`xxx作为备注（比如这里的new-commit），此时`local git`本地仓库中的`my-feature`分支与磁盘`disk`代码相同。

  ![](C:\Users\91077\AppData\Roaming\Typora\typora-user-images\image-20231117165350533.png)

- 此时本地的`local git`已经知晓变化，然而github目前并不知道。我们需要把这个`local git`的变化告知github。使用的命令就是`git push`

  ![image-20231117170610525](C:\Users\91077\AppData\Roaming\Typora\typora-user-images\image-20231117170610525.png)

  ```bash
  # 命令格式如下，关于远程仓库名可以通过 git remote查看
  git push <remote_repository_name> <local_branch>:<remote_branch>
  
  # 若远程仓库增加的是新的分支，可以简化为
  git push <remote_repository> <local_branch>
  # local_branch和remote_branch名字相同。
  ```

  - 我们可以通过`git remote`相关命令查看、添加、重命名和删除远程仓库的功能。

  - ```bash
    git remote #列出当前仓库已配置的远程仓库
    git remote -v #列出当前仓库中已配置的远程仓库，并显示它们的 URL
    git remote add <remote_name> <remote_url># 添加一个新的远程仓库。指定一个远程仓库的名称和 URL，将其添加到当前仓库中。
    git remote rename <old_name> <new_name># 将已配置的远程仓库重命名。
    git remote remove <remote_name> # 从当前仓库中删除指定的远程仓库。
    git remote set-url <remote_name> <new_url> # 修改指定远程仓库的 URL。
    ```

  查看远程仓库名称

  ![image-20231117182043678](C:\Users\91077\AppData\Roaming\Typora\typora-user-images\image-20231117182043678.png)

  `push`到远程仓库

  ![image-20231117182631226](C:\Users\91077\AppData\Roaming\Typora\typora-user-images\image-20231117182631226.png)

  查看所有的分支`git branch -a`

  ![image-20231117182903114](C:\Users\91077\AppData\Roaming\Typora\typora-user-images\image-20231117182903114.png)

- 当我们提交完`my-feature`后发现，远程仓库的`main`branch又多了`update`这个commit![image-20231117195420126](C:\Users\91077\AppData\Roaming\Typora\typora-user-images\image-20231117195420126.png)

  我们这个新的功能分支是在原本`main`分支下衍生的，那么我们就需要知道在如今的`main`分支又增加了新的commit后是否还有效。因此我们需要将`main`branch的更新同步到`my-feature`这个branch中。

  - 我们`local git`里的`main`branch 和`remote`仓库里的`main`branch是不一样的，因此首先我们需要切换到`main`这个branch中（`git checkout main`），这时候我们硬盘里的源代码处于`local git`下`main`分支下`init`状态。

  - 在从原本的`my-feature`分支转换到`main`分支后，就需要使用`git pull`命令

    - `git pull`用于从远程获取代码并合并本地的版本‘

    - `git pull`是`git fetch`和`git merge FETCH_HEAD`的简写，`FETCH_HEAD`是最近一次`git fetch`获得的内容。

    - ```bash
      # 命名格式如下
      git pull <remote_repository_name> <remote_branch>:<local_branch>
      # 同一个名字的branch，简化为
      git pull <remote_repository_name> <branch_name>
      ```

    运行`git pull my_repository main`,这样子就把远端的`main`同步到了我们`local git`里的`main`![image-20231117202141276](C:\Users\91077\AppData\Roaming\Typora\typora-user-images\image-20231117202141276.png)

  - 然后我们便需要回到我们的`my-feature`这个分支（`my-feature`是在原本`main`分支只有一个`init`commit时复制创造的），因此要仍然要在`remote`下的`main`分支下继续能够生效我们的功能分支，如图：![image-20231117203105020](C:\Users\91077\AppData\Roaming\Typora\typora-user-images\image-20231117203105020.png)

    在`my-feature`需要使用命令`git rebase main`，思路如下

    - git会从`main`和`my-feature`的共同祖先（也就是`main`分支`init`后我们创建了新的功能分支`my-feature`,这个`init`就是共同祖先）开始提取`my-feature`分支上的修改，也就是`my-feature`在`init`后的修改。![image-20231117204649982](C:\Users\91077\AppData\Roaming\Typora\typora-user-images\image-20231117204649982.png)

    - 然后把`main`在共同祖先后的修改拿过来，接入到`my-feature`的`init`后。![image-20231117204723552](C:\Users\91077\AppData\Roaming\Typora\typora-user-images\image-20231117204723552.png)

    - 接着在这个最新修改的基础之上，再把我之前的`new-commit`弄回去。

      在这个rebase过程中，会出现`rebase conflit`，这时候就需要手动地选择你到底要哪一块代码，在rebase成功后我们的`my-feature`branch就变成了现在这个样子![image-20231117204912185](C:\Users\91077\AppData\Roaming\Typora\typora-user-images\image-20231117204912185.png)

      这里的新的红色的`new-commit'`与原本蓝色的`new-commit`内容并不一定相同，因为这是处理`rebase conflit`后的结果。

    - 转换到`my-feature`分支后，通过调用`git rebase main`，相当于在最新的`main`分支上做了我们的修改。

    - 最后我们需要将`local git`的`my-feature`同步到`remote`远程仓库当中。由于我们使用了`rebase`，因此`git push`命令要加上`-f`，表示强行（force）push，使用`git push -f my-repository my-feature`

      ![image-20231117210300668](C:\Users\91077\AppData\Roaming\Typora\typora-user-images\image-20231117210300668.png)

- 到此一切准备就绪，我们就需要将我们更新的代码合并到了这个`main`branch当中了，这个过程叫做`pull request`

  - 我们主观地认为，这个主分支是属于项目的，不属于任何个人，而功能分支也就是所谓的`feature branch`是属于个人的。
  - 尽管这个`feature branch`的主人和这个项目的主人可能是同一个人，但是这两个分支上他们是不同的角色
  - `pull request`的意思是request这个项目的主人，把我这个新的分支的改变，给pull到这个项目里，也就是请求`main`branch 将你的`my-feature`branch上面的改动给pull进去。
  - 在这个`main`branch的维护者，审查了你的代码后，一般情况下会使用`squash and merge`,也就是将这个`feature` branch上所有的改变合并成一个改变，然后把这个commit放到`main`branch上

### git撤销操作

使用git的时候，我们一般会涉及到4个区域，分别是我们的`硬盘disk(工作区)`、`暂存区Staging`、`Local(本地版本库)`、`remote(远程仓库)`，现在我们假设这四个区域是同步的，都只有一个`init`commit。

![image-20231118150236292](C:\Users\91077\AppData\Roaming\Typora\typora-user-images\image-20231118150236292.png)

现在我对我的代码文件做了一些修改，这时候你用`git diff`是可以看到你的修改的（也就是修改后的文件和`local git`版本库保存的文件有何不同），你使用`git status`（查看目前git仓库，包括有关未提交的更改，这里的git仓库都指的是本地的`local git`仓库），你会发现这个修改的文件处于`Changes not staged for commit`

![image-20231118150542120](C:\Users\91077\AppData\Roaming\Typora\typora-user-images\image-20231118150542120.png)

#### 1. 工作区的文件修改撤销

现在我发现我在`硬盘disk(工作区)`的修改是错误的，我想要撤销对此文件的修改

![image-20231118151637548](C:\Users\91077\AppData\Roaming\Typora\typora-user-images\image-20231118151637548.png)

#### 2. 暂存区的文件撤销修改

如果我们对`硬盘disk`的修改完成，使用`git add <changed_file>`命令，那么这个修改便会同步到至`暂存区Staging`，这时候你再使用`git status`便会发现文件处于`Changes to be committed`

![image-20231118152413202](C:\Users\91077\AppData\Roaming\Typora\typora-user-images\image-20231118152413202.png)

在这种情况，若我们想要把这个修改从`暂存区Staging`移除，但还保留`硬盘disk`上的修改，也就是我们想要撤销`git add`这个同步到`暂存区`的操作，我们可以使用`git reset <changed_file>`命令![image-20231118153025938](C:\Users\91077\AppData\Roaming\Typora\typora-user-images\image-20231118153025938.png)

如果你就是想要撤销这个文件的所有修改，包括`暂存区`和`硬盘disk`上的修改，你可以使用`git checkout HEAD <changed_file>`(这个`HEAD`在git里面表示最近一次的commit状态，在这里就是Init)，这个操作会让你丢失`硬盘`上的修改。

![image-20231118153223332](C:\Users\91077\AppData\Roaming\Typora\typora-user-images\image-20231118153223332.png)

#### 3. local git上文件的撤销

当你使用`git commit`将`暂存区`的文件修改同步到`local git`上，那么你的修改就正式变成了一个commit放在了`local git`上。

![image-20231118153924822](C:\Users\91077\AppData\Roaming\Typora\typora-user-images\image-20231118153924822.png)

在这种情况下，如果我们只是想单纯地撤销这个commit，可以使用`git reset --soft HEAD~1`,`HEAD`表示最近的一次commit，而`HEAD~1`则代表最近一次commit再前一次的commit状态，执行完这个命令之后，表示`local git`回到了`HEAD~1`的状态，而你的硬盘里的文件并不会改变。

![image-20231118162453958](C:\Users\91077\AppData\Roaming\Typora\typora-user-images\image-20231118162453958.png)

如果使用`git reset HEAD~1`等价于`git reset --mixed HEAD~1`，它会同时撤销`暂存区`和`local git`里的文件修改，相当于同时撤销了这个文件的`git add`和`git commit`操作。

![image-20231118163211365](C:\Users\91077\AppData\Roaming\Typora\typora-user-images\image-20231118163211365.png)

如果更进一步，连并将`硬盘上disk`上文件的修改一起撤销，使用`git reset --hard HEAD~1`

![image-20231118164151799](C:\Users\91077\AppData\Roaming\Typora\typora-user-images\image-20231118164151799.png)

#### 4.git revert 取消指定的commit提交内容

`git reset`可以让你退回到之前任意一个commit的状态，在我们完成`git commit`之后，我们还有另外一种形式的撤销，即`git revert`，和`git reset` 不同，`git revert`本质上是在给你增加一个commit，而这个commit的效果，恰好是你指定commit效果的反过来。下图我们把change1的反作用的commit叫做-change1。

![image-20231118165426700](C:\Users\91077\AppData\Roaming\Typora\typora-user-images\image-20231118165426700.png)

`git revert`命令的参数是一个或者多个commit，上图中给的参数是HEAD，HEAD也就是最近的commit也就是change1。

#### 5. `git revert` 相比`git reset`有什么好处

- `git reset`只能退回到之前某一个commit的状态，而`git revert`可以撤销中间任意一个commit。![image-20231118170303719](C:\Users\91077\AppData\Roaming\Typora\typora-user-images\image-20231118170303719.png)

  例如，现在我们有两个commit分别为`change1`和`change2`，假设这个change的hash是70a0....，zh这个时候我们可以用`git revert 70a0`,再这个链上增加一个-change1的commit，那么最终的结果就相当于在`Init` 直接增加了 `change2`的commit,当然此时你的HEAD状态便是`-change1`。

- 当我们把`local git`的这些修改用`git push`，同步到了远端，那么这个修改就正式到了远端。

  ![image-20231118171423653](C:\Users\91077\AppData\Roaming\Typora\typora-user-images\image-20231118171423653.png)

  此时我们就要判断我们的分支是属于公有分支（只要不止你一个人在使用这个分支）还是个人分支。对于公有分支，只能增加commit不能减少的，因为你一旦做了删除操作，别人的分支就乱了套了。

  因此当我们修改的分支是一个公有分支时，我们只能使用`git revert`命令在这个公有分支上增加一个commit，从结果上撤销我们之前的修改。

  ![image-20231118172243788](C:\Users\91077\AppData\Roaming\Typora\typora-user-images\image-20231118172243788.png)

  如果是你的个人分支的话（只限于个人分支！），你可以直接将你这个change的commit砍掉(直接使用`git reset --hard HEAD~1`)，再使用`git push -f`，这里必须添加`-f`，因为你正常分支进行push时，会发现你这个分支比原本的分支少，因此使用`-f`强制进行push。

  ![image-20231118172825661](C:\Users\91077\AppData\Roaming\Typora\typora-user-images\image-20231118172825661.png)

### Git 与VScode

#### git clone 和GitHub上直接download zip区别

download zip 是直接下载解压的是一个单纯的文件夹，而git clone 拉取下来的是仓库，区别在于是否具有隐藏文件.git

![image-20231116205803228](C:\Users\91077\AppData\Roaming\Typora\typora-user-images\image-20231116205803228.png)

若刚开始在本地开发的项目就是一个纯文件夹，我们可以使用

`git init # 将本地文件夹变为一个git仓库`

#### Git的工作流程

==工作区== <u>通过 git add  <file></u>  ---> ==暂存区== 	<u>通过 git commit</u>   ---> ==版本库（仓库）==

我们使用vscode打开刚刚`git init`的文件夹，因为vscode集成了`git bash`的功能。

![image-20231116233750679](C:\Users\91077\AppData\Roaming\Typora\typora-user-images\image-20231116233750679.png)

我们可以使用

`git add`命令将工作区的文件转移到暂存区，如果是所有的文件，则可以输入命令

`git add -A  #将所有文件放到暂存区`

![image-20231116234804113](C:\Users\91077\AppData\Roaming\Typora\typora-user-images\image-20231116234804113.png)

提交到仓库的话，使用==git commit - m "xxxxx"== 其中的xxx是每次提交的描述信息

![image-20231116235508267](C:\Users\91077\AppData\Roaming\Typora\typora-user-images\image-20231116235508267.png)

在提交到仓库时，你需要设置你的user.email 和 user.name（是为了将提交关联到特定的用户，这两个设置项可以帮助版本控制系统（比如 Git）知道是谁进行了特定的更改。）

使用==git log -stat== 查看详情。

![image-20231117000335894](C:\Users\91077\AppData\Roaming\Typora\typora-user-images\image-20231117000335894.png)

当然你可以安装==GitLens==更容易查看

![image-20231117000448802](C:\Users\91077\AppData\Roaming\Typora\typora-user-images\image-20231117000448802.png)

![image-20231117000619931](C:\Users\91077\AppData\Roaming\Typora\typora-user-images\image-20231117000619931.png)

#### Git checkout 和 Git reset

-  **git checkout** 命令用于在不同的分支之间切换、恢复文件、创建新分支等操作。

假设你修改了你的某个文件，例如：

![image-20231117001339746](C:\Users\91077\AppData\Roaming\Typora\typora-user-images\image-20231117001339746.png)

此时我们还处于==工作区== 那么我们采取以下的方式：

```bash
# 切换到指定的分支branch，比如main分支
git checkout <branch-name>
git checkout main 
# 切换到上一个分支
git checkout -
# 创建一个新分支 <new-branch-name> 复制当前的branch到新分支上，并立即切换到新创建的分支
git checkout -b <new-branch-name>
# 将工作区指定文件 <file> 恢复到最新的提交状态
git checkout -- <filename>
```

`git checkout -- <filename>`只对==工作区==的代码有效，有两种场景

- 一种是file文件 修改时还未`git add`到暂缓区当中，使用`git checkout -- file `的话就会将工作区的内容回退到上一次`git commit`的状态（其实也就是修改被清除）。例如![image-20231117020403582](C:\Users\91077\AppData\Roaming\Typora\typora-user-images\image-20231117020403582.png)通过`git checkout -- main.cpp`后![image-20231117020452176](C:\Users\91077\AppData\Roaming\Typora\typora-user-images\image-20231117020452176.png)
- 另外一种是file文件修改完已经`git add`到暂缓区中，此时工作区又做了修改。![image-20231117015925951](C:\Users\91077\AppData\Roaming\Typora\typora-user-images\image-20231117015925951.png)此时我们可以看到`Staged Changes（暂缓区）`和`Changes(工作区)`均有修改。那么再调用`git checkout -- main.cpp`，工作区的代码会回退到上一个`git add`的状态，也就和`Staged Changes`里的main.cpp一样。![image-20231117020249285](C:\Users\91077\AppData\Roaming\Typora\typora-user-images\image-20231117020249285.png)

- **git** **reset** 命令用于回退版本，可以指定退回某一次提交的版本。

比如我们修改了一个文件，并且已经commit到了版本库，那么就可以使用==git reset==进行回撤。

![image-20231117011118936](C:\Users\91077\AppData\Roaming\Typora\typora-user-images\image-20231117011118936.png)

```bash
# 基本格式如下，默认为--mixed，其他内容用到时再去翻阅
git reset [--soft | --mixed | --hard] [HEAD]

# 回退所有内容到上一个版本 
# HEAD表示当前版本，以下命令效果相同
git reset HEAD^
git reset HEAD~1

# 拉取最近一次提交到版本库的文件到暂存区  该操作不影响工作区
git reset HEAD^ main.cpp

# 回退到任意一个版本
HEAD^ == HEAD~1 上个版本

HEAD^^ ==HEAD~2 上上个版本

以此类推
```

当我执行 `git reset HEAD~1 main.cpp` 后，但是 `Staged Changes(暂缓区) `中`main.cpp`为`first commit`的状态。而工作区仍然是`second commit` 的状态，未被修改。

![image-20231117013111591](C:\Users\91077\AppData\Roaming\Typora\typora-user-images\image-20231117013111591.png)

而执行 `git reset HEAD~1`则直接删除了`second commit`.

### GCC、gcc和g++区别

`GCC`：GNU Compiler Collection（GNU编译器集合），可以编译C、C++、JAV、Fortran、Pascal等语言。

`gcc`：是GCC中的GNU C Compiler（C编译器）

`g++`：是GCC中的GNU C++ Compiler （C++编译器）

`gcc`和`g++`的主要区别

- 下面的编译包括编译和链接阶段。

- 对于`*.c`和`*.cpp`文件，`gcc`会分别当作`c`和`cpp`文件编译
- 而`g++`面对`c`和`cpp`文件，`g++`会统一当作`cpp`文件编译
- 使用`g++`编译文件时，`g++`会自动链接标准库STL，而`gcc`不会自动连接`STL`
- `gcc`在编译`c`文件时，可使用的预定义宏是比较少的。
- `gcc`在编译`cpp`文件时/`g++`在编译`c`文件和`cpp`文件时（这时候`gcc`和`g++`调用的都是`cpp`文件的编译器），会加入一些额外的宏。
- 在用`gcc`编译`cpp`文件时，为了能够使用STL，需要加参数 `–lstdc++ `，但这并不代表 `gcc –lstdc++ `和 `g++`等价，它们的区别不仅仅是这个。

1. 误区一:`gcc`只能编译`c`代码,`g++`只能编译`c++`代码

   `*.c`文件，`gcc`把它当作是C程序，而`g++`当作是c++程序；后缀为`.cpp`的，两者都会认为是`c++`程序，并且注意，虽然c++是c的超集，但是两者对于语法的要求是有区别的，c++更为严格。==g++是专门用于编译c++代码，但是用gcc也可以编译c++代码，gcc主要是c编译器，但是也提供对c++的支持，也可以进行语法检查，但是在编译的链接阶段，gcc并不如g++那么完善，需要手动链接C++标准库。==

   在链接阶段，由于`gcc`命令不能自动和c++程序使用的库链接，所以通常使用`g++`来完成链接，

   `gcc -o output_filename source_filename.cpp -lstdc++`

   - `gcc` 在编译 `source_filename.cpp` 时会产生中间目标文件，并且 `-lstdc++` 用于链接 C++ 标准库。`-o output_filename` 部分将这些中间目标文件链接在一起生成最终的可执行文件 `output_filename`。

2. 误区二：编译只能用`gcc`，链接只能用`g++`

   编译可以用`gcc`/`g++`，而链接可以用`g++`或者`gcc -lstdc++`。因为`gcc`命令不能自动和C++程序使用的库链接，所以通常使用g++来完成链接。

### 一个程序 从源文件 到可执行文件的过程

- 预处理
  - **gcc -E *.c > *.txt**  一般是不保存，可以通过>重定向到txt文件中
    - 预处理主要做的是头文件的引入、宏的展开、指令的处理
- 编译
  - 编译时，编译器需要的是语法的正确，函数与变量声明的正确，对于后者，通常是你需要告诉编译器头文件的所在位置（头文件中应该只是说明，而定义应该放在C/C++文件中），只要所有的语法正确，编译器就可以编译出中间目标文件（Windows下是`.obj`文件，UNIX下是`.o`文件）。
  - **gcc -c *c** 会自动生成 ***.o** 的目标文件
    - **.o** 包括静态库 动态库  部分可以看作SDK 
- 链接
  - 链接时，主要是链接函数和全局变量，使用中间目标文件（`.o`文件或者`.obj`文件）来链接我们的应用程序。
  - 链接器并不管函数所在的源文件，只管函数的目标中间目标文件（Object File），在大多数的时候，由于源文件太多，编译生成的中间目标文件太多，而在链接时需要明显地指出中间目标文件名，这对编译很不方便，所以我们要给中间目标文件打个包，在Windows下这种包叫做`库文件(Library File)`，也就是`.lib`文件，在UNIX下，是`Archive File`，也就是`.a`文件。
  - **gcc main.o A.o B.o C.o -o main.exe**
    - 把多个目标文件，包括动态库、静态库链接到一起，生成最终的可执行文件
- 总结
  - 源文件首先会生成中间目标文件，再有中间目标文件生成可执行文件。
  - 在编译时，编译器只检测程序语法和函数、变量是否被声明。如果函数未被声明，编译器会给出一个警告，但是仍让可以生成Object File，而在链接程序时，链接器会在所有的Object File中寻找函数的实现，如果找不到，那么便会报链接错误码`Linker Error`。

### makefile

它通常被用于告诉构建工具（如 `make`）如何编译和链接源代码，以及如何生成最终的可执行文件或库文件。

首先，我们用一个示例来说明makefile的书写规则，以便给大家一个感性认识。这个示例来源于gnu的make使用手册，在这个示例中，我们的工程有8个c文件，和3个头文件，我们要写一个makefile来告诉make命令如何编译和链接这几个文件。我们的规则是：

1. 如果这个工程没有编译过，那么我们所有的c文件都要被编译并被链接
2. 如果这个工程的某几个c文件被修改，那么我们只编译被修改的c文件，并链接目标程序
3. 如果这个工程的头文件被改变，那么我们需要编译引用了这几个头文件的c文件，并链接目标程序。

只要makefile写的好，那么make命令会自动智能地识别当前文件修改的情况来确定哪些文件需要重编译，从而自动编译所需要的文件，并链接目标程序。

#### makefile的规则

```bash
target... : prerequisites...
	recipe
	...
	...
```

- `target`：可以是一个`object file`（目标文件），也可以是一个可执行文件，还可以是一个标签`label`（标签特性，会在后续的==伪目标==）章节中会有叙述。
- `prerequisites（先决条件）`：生成该`target`所依赖的文件
- `recipe（方法）`：该`target`要执行的命令（任意的`shell`命令）。

这是一个依赖关系，也就是`target`这一个或者多个的目标文件，依赖于`prerequisites`中的文件，其生成`target`的方法则定义在`recipe`中。

那么当`prerequisites`中有一个以上的文件要比`target`文件要新的话（ 有文件被修改了），`recipe`所定义的命令就会被执行 。

#### 一个示例

如果有一个工程有3个头文件和8个c文件，那么makefile应该为下面这个样子：

```bash
edit : main.o kbd.o command.o display.o \
        insert.o search.o files.o utils.o
    cc -o edit main.o kbd.o command.o display.o \
        insert.o search.o files.o utils.o

main.o : main.c defs.h
    cc -c main.c
kbd.o : kbd.c defs.h command.h
    cc -c kbd.c
command.o : command.c defs.h command.h
    cc -c command.c
display.o : display.c defs.h buffer.h
    cc -c display.c
insert.o : insert.c defs.h buffer.h
    cc -c insert.c
search.o : search.c defs.h buffer.h
    cc -c search.c
files.o : files.c defs.h buffer.h command.h
    cc -c files.c
utils.o : utils.c defs.h
    cc -c utils.c
clean :
    rm edit main.o kbd.o command.o display.o \
        insert.o search.o files.o utils.o
```

反斜杠`\`是换行符，便于makefile的阅读，把这个内容保存在名字为makefile，然后在该目录下直接输入命令`make`即可生成执行文件edit，执行`make clean`可以删除可执行文件和所有的目标文件。

在这个makefile中，目标文件（target）包含：可执行文件edit和中间目标文件（`*.o`），依赖文件（prerequisites）即为冒号后面的`.c`文件和`.h`文件。 每一个`.o`

通常包括`目标`、`依赖项`、`命令`组成，一个简单的makefile如下

```bash
main.exe: main.o func.o
    gcc main.o func.o -o main.exe

main.o: main.c
    gcc -c main.c -o main.o

func.o: func.c
    gcc -c func.c -o func.o
```

然后在命令行中使用`make`就可以实现自动化的编译和构建过程

```bash
main.exe: main.o A.o B.o
	gcc *.o -o $@
%.o:%.c
	gcc -c $< -o $@
```

这些规则使用了一些 Makefile 的常用语法和通配符：

- `$@`：代表规则的目标，即要生成的目标文件名。
- `$<`：代表规则中的第一个依赖项，即输入文件名。





你为什么选择我们岗位：

我想去接触网络工程中在实际开发场景下，一些硬件基础设施、智能监控与预警相关的所做的技术，想要从实际开发中进行学习能够对系统架构有一定的接触，能够与字节这样的团队一起成长。

### jetson nano烧录

去Nvidia官网上下载Nvidia SDK Manager，然后插入自己的SD卡，将jetson nano的配置文件（比如jetson 的系统镜像，Jeston SDK componets 这些包括各种推理部署的组件，比如CUDA、CUDNN 、TensorRT和Deepstream）通过SDK Manager对SD卡进行烧录，最后将SD卡插入到jetson nano的卡槽上，jetson nano会通过SD卡进行引导，安装操作系统。

### 模型部署在Jetson nano的过程

- 模型的训练我是在自己电脑上进行训练的，训练完的pytorch模型，使用onnx-simplifer来简化优化网络模型（折叠常量（消除结果恒为常量的算子）和图变换（合并图层）的方式），再将简化优化后的onnx网络模型通过TensorRT进行量化，得到tensorRT格式的engine文件，最后部署到deepstream上。
  - TensorRT加速的原理：TensorRT在推理阶段可以使用精度低（INT8）的数据类型进行运算。
  - 图层与张量的融合
  - 什么是deepstream，DeepStream与TensorRT结合可以实现多视频流的实时推理加速。
  - 为了模拟摄像的接入，我们购买了摄像头IMX219，可以通过deepstream配置文件的CSI接口接入。

- 在jetson nano上根据其nvidia驱动的版本配置模型的环境（CUDA、CUDANN、安装Pytorch），Nvidia的Deepstream视频流框架是支持jetson nano的，在nvidia SDK Manager烧录时就已经携带了。
- 将训练的模型导入到jetson nano上
- 去github下载deepstream-yolo，使用其给的模型转换程序将pytorch模型获得cfg和wts的文件。
- 修改deepstream配置文件deepstream_app_config.txt，可以对控制显示的布局，比如3行两列就是6路视频，在通过添加source添加是视频流的来源，视频流的类型以及读取方式（rtsp推流），在推理配置文件config_infer_primary.txt中可以配置模型的参数，可以配置TensorRT文件，或者通过之前模型转换的wts和cfg文件自动生成engine文件，通过labels添加目标检测模型的标签。
- 最后通过deepstream可以直接进行运行。



## -1. 深度学习基础

### 1. 什么是卷积？

对图像和滤波矩阵（一组固定的权重，可以看作一个恒定的滤波器filter）做内积（逐个元素相乘再求和）的操作。

### 2. 什么是卷积神经网络CNN的池化层pool层？

在卷积神经网络中，池化层是一种用于降低特征图尺寸的操作，池化层通过在特定区域内采样（最大池化取池化窗口中的最大值，平均池化计算池化窗口所有值的平均值），保留主要特征的前提下，减小特征图的尺寸大小，减少模型的参数量，降低模型的计算复杂度，可以提高模型的鲁棒性。

### 3. 下采样和上采样

下采样就是指减小特征图的空间大小，通常通过池化层，现在通过设置步长为2的卷积也可以实现。

上采样指的是扩大特征图的空间尺寸，可以通过插值、转置卷积的方法来实现。

### 4. 非线性激活函数

- 学习抽象层次的特征和拟合复杂的数据：如果不引入非线性激活函数，那么整个网络相当于一个线性模型，无法捕捉复杂的非线性关系，引入非线性激活函数，可以使网络模型能够逐渐学习到更抽象层次的特征，也能够更好地拟合复杂的数据
- 梯度传播：在反向传播算法中，梯度（即损失函数对于参数的导数）用于更新网络的权重，激活函数的非线性性质确保了梯度可以在网络中传播，使得网络可以学习到正确的权重。如果使用非线性，梯度将会始终相同，导致网络无法学习复杂的模式。

### 5. 什么是过拟合，什么是欠拟合

- 过拟合是指在模型在训练集上表现很好，但是在新数据集上表现较差的现象（泛化能力差），这是由于模型学习到了训练数据的噪声和细节，而忽略了数据的复杂度，模型试图你和每个训练样本的特殊特征
  - 增加训练的数据量：提供更多的训练样本，减少噪声对模型的影响。
  - 简化模型减少模型的复杂度，减少网络层数
  - 正则化
- 欠拟合是指模型未能在训练数据上学到更多的信息，导致在训练数据和新数据上表现都很差，当模型过于简单或者没有足够的训练数据时，模型无法捕捉到数据的复杂关系。
  - 增加模型的复杂度
  - 增加数据量

### 6. 正则化



## 0、项目准备

### 0. batch和epoch

- batch：每一个batch（批次）指的是在训练过程中，一次性输入到神经网络的一组数据。
  - 例如，如果你的训练数据集有1000张图像，批次大小设置为32，那么每一个batch就包含32张图像。神经网络根据这个batch的数据进行一次前向传播（计算预测值），然后进行一次反向传播（计算梯度并更新权重），从而完成一次参数更新。
- epoch：每一个epoch（周期）指的是神经网络完成了在整个数据集上进行了一次前向传播和反向传播，一个epoch包含多个batch，每个batch上的参数更新会累积到整体的模型参数中。

### 1. 模型的构建你是从哪些方面进行考虑，又分别做了哪些工作？

模型的构建我主要是从三个方面进行考虑，一个是模型的精度、二是模型的速度、三是模型的大小

- 在精度优化上我主要是从三个方面进行的

  - 1.数据分析与处理：在数据分析与处理，我主要是做了数据清洗、离线数据扩充以及在线数据增强的工作。

    - 数据清洗：具体所做的事就是：企业进行命题时给了10个监控摄像的视频，对这些监控摄像的视频进行视频抽帧就会存在大量的静态帧，因此我们删除了部分的静态帧，减小模型对静态帧的过拟合，除此之外，还删除了过于模糊的图片，来避免对网络权重的损坏。
    - 离线数据扩充：具体所做的事有两件：一个就是对数据集进行类别数量统计，发现了样本类别不均衡的问题，若直接训练的话会破坏网络的权重并且不利于收敛，另外一个就是通过图像裁剪、图像平移、图像缩放以及添加噪声的方式，将数据集扩充到4000张。
    - 在线数据增强：为了进一步提高模型的鲁棒性（抗干扰能力）以及泛化能力和缓减工业检测样本较少的问题，我采用了Mosaic数据增强的方式，即在训练过程中，每一个batch会从随机选择四张不同图像，四张图像可以采用随机裁剪、缩放的方式，最后拼接到一起生成新的训练样本。

  - 2.主干网络的选择：

    主干网络的选择主要是选择了

  - 3.Neck网络的融合

## 一、计算机网络

### 集线器、交换机、和路由器的作用以及区别

- 集线器Hub：
  - 工作在物理层
  - 作用：集线器Hub是一种简单的网络设备，集线器是一个广播设备，它收到的数据包会在所有的端口之间广播
  - 特点：不做任何的决策，只是简单地将收到的数据包广播到所有连接的设备上
- 交换机Switch
  - 工作在数据链路层，它可以理解和处理数据链路层的数据帧，根据MAC地址学习和转发数据
  - 作用：交换机Switch是一种智能设备，它根据数据包的目的地址（MAC地址）将数据包定向发送到特定端口，而不像集线器Hub广播到所有的端口
  - 智能，减少网络拥塞和碰撞
- 路由器Router
  - 工作在网络层
  - 作用：路由器是用于连接多个网络并在它们之间传输数据包的设备，它在网络层进行操作，根据目的地址（IP地址）来选择传输路径，决定数据如何在不同网络间转发
  - 特点：路由器能够连接不同类型的网络，例如连接局域网到互联网，它具有路由功能，同时提供网络安全
- 总结
  - 集线器作用在物理层，交换机作用在数据链路层，而路由器作用在网络层
  - 集线器只是简单地传输信号，交换机能够理解MAC地址并选择性地传输数据，而路由器能够理解IP地址并根据路由表选择最佳路径传输数据。





### 1.在浏览器地址栏输入一个URL后回车，背后会进行哪些操作？

浏览器地址中输入URL并且获取响应的过程，其实就是浏览器和URL对应的服务器通信的过程。

应用层：

- 首先是URL解析，将网址中的协议（http/https）、域名（www.baidu.com）、端口号、请求资源的路径以及查询参数等。
- 然后对URL解析的信息域名、端口号以及请求资源的路径封装成http请求报文。
- 通过DNS域名解析获取目标服务器的地址。

传输层：

- 根据目标服务器的IP以及端口号，建立浏览器与目标服务器的TCP连接。
- TCP三次握手完成后，浏览器便可以向目标服务器发送http请求
- 把应用层传过来的http请求报文按序号分割成若干报文段并加上TCP首部，转发给网络层。

网络层：

- IP协议将TCP报文段添加IP首部封装成IP数据报，再利用ARP协议根据IP地址获取MAC地址后后转发给链路层

服务器收到这些报文段后，按照序号以原来的顺序重组http请求报文，然后处理该请求并返回http响应报文。浏览器接收响应报文后解析并渲染页面。

最后浏览器和服务器之间不再发送数据后，四次挥手断开TCP连接。

### 2. TCP和UDP的使用场景

UDP是用户数据报协议，在传输数据之前不需要建立连接，UDP不提供可靠的传输，适用于实时性需求较高的场景，例如语音、视频、直播。

TCP是传输控制协议，在传输之前需要通过三次握手建立连接，传输过程中，通过序号和确认号、数据校验（校验和）、超时重传（定时器）、窗口机制、拥塞控制来保证可靠传输。在数据传输结束后，四次挥手关闭连接节约资源。TCP适用于可靠性需求较高的场景，例如发送文件、邮件等。

### 3. TCP三次握手

刚开始客户端的状态为closed，服务端的状态为listen（侦听来自客户端的TCP连接请求）。

1.第一次握手，客户端向服务端发送SYN报文，设置自己的初始序列号ISN=x，序号seq=x，然后状态变成同步已发送SYN_Sent状态。

2.第二次握手，服务端接收到了客户端发来的SYN报文，回复SYN+ACK报文，ACK设置为1，ack=客户端发送的SYN报文序列号+1，表示对客户端发送的SYN报文的应答，同时设置自己的初始序列号ISN=y，序列号seq=y。状态由listen状态转为同步已接受SYN_Received状态。

3.第三次握手，客户端收到了服务端发来的SYN+ACK报文，会发送一条ACK报文给服务端，ACK设置为1，ack=服务端ISN初始序列号+1，表示确认收到服务端的SYN+ACK报文。此时客户端的状态由同步已发送SYN_Sent变为Established状态。服务端接收到了客户端的ACK报文，状态也变成Established状态。自此三次握手完成，TCP建立连接。

### 4. 为什么要三次握手？

三次握手的目的就是要让双方都知道自己与对方的接收和发送能力没有问题。

第一次握手（客户端发送SYN报文，服务端接收该报文）：服务端知道客户端的发送能力和自己的接收能力没有问题。

第二次握手（服务端发送SYN+ACK报文，客户端接收该报文）：客户端知道客户端和服务端的发送和接收能力均没有问题，但是客户端还未完全确认。

第三次握手（客户端发送ACK报文，服务端接收该报文）：服务端和客户端此时都确认了双方的接收和发送能力没有问题。

### 5. ISN是否能够固定？

三次握手的一个重要的功能就是客户端和服务端互相交换ISN初始序列号，以便双方接收数据时知道如何按序列号拼接。

若ISN固定，那么攻击者很容易猜出后续的序列号，从而进行恶性的攻击

### 6. 半连接队列和全连接队列

当服务端收到客户端的SYN报文，回复SYN+ACK报文，此时服务端的状态由listen转为SYN_Received同步已接收状态。此时服务端处于并未完全建立连接，若有其他的客户端的TCP连接请求，便会放入到半连接队列当中。

全连接队列，则是指，当服务端进入Established状态，客户端与服务端完全建立TCP连接，此时若有其他客户端发来TCP连接请求，便会放入到全连接队列当中。

### 7. 三次握手可以携带数据吗？

第一次与第二次均不可以携带数据，第三次可以携带数据。

假如第一次可以携带数据，若有人恶意攻击服务器，并且在每次发送的SYN报文中都携带大量的数据，然后疯狂地发送SYN报文，这会让服务器花费大量时间以及内存空间去处理这些报文。

然而在第三次握手时，客户端已经知道服务端和客户端的接收和发送能力都是没有问题的，因此向服务端发送ACK报文可以携带数据。

### 8.如果第三次握手丢失了，该如何处理。

服务端发送SYN_ACK报文后，久久未收到客户端的ACK报文，并会触发TCP的超时重传机制，重新地发送SYN_ACK报文，若超过设定的最大重传次数仍未收到客户端的ACK报文，便会关闭连接，将该请求从半连接队列中删除。

### 9.TCP四次挥手

刚开始，客户端和服务端的状态都为Established，由于TCP是全双工通信，因此客户端和服务端均可主动发起关闭连接请求。

假设客户端率先发起关闭连接请求。

1.第一次挥手。客户端向服务端发送FIN报文请求连接终止，报文会指定一个序列号seq=u，客户端不再向服务端发送数据，关闭客户端到服务端的TCP连接，状态由Established变成FIN_Wait1。等待服务器的确认。

2.第二次挥手，服务端接收到了客户端的FIN请求连接终止报文，发送ACK报文作为应答，ACK设置为1，ack=u+1，表明收到了客户端的FIN报文。此时服务端的状态从Established变成Cloes_Wait，客户端收到服务端的ACK报文后，状态变成FIN_Wait2。此时TCP处于半关闭状态，客户端到服务端的连接关闭。

3.第三次挥手，当服务端不再向客户端发送数据，向客户端发送FIN报文请求终止连接，指定一个序列号seq=v。状态由Close_Wait状态变成Last_Ask状态，等待客户端的确认。

4.第四次挥手，客户端收到了服务端的FIN报文，回应一个ACK报文，ACK=1，ack=v+1。状态由FIN_Wait2变成Time_Wait。服务端接收到了客户端的ACK报文后，状态进入Closed状态。在经过等待计时器设置的时间2MSL（最大报文生存时间 Maximum Segment Lifetime），也就是一个报文的来回时间后，客户端进入Closed状态。若服务端未在规定的时间收到客户端的ACK报文，便会重现发送FIN报文给客户端，客户端也会重新发送ACK报文。

TIME_WAIT状态，等待2倍的最大报文生存时间（2MSL，Maximum Segment Lifetime），这段时间内网络中的所有可能滞留的报文段都应该被丢弃，以保证新的连接不会被这些滞留的数据影响。这样的设计可以避免在新的连接中混入旧的报文段，确保连接的安全关闭。

### 10. 为什么要四次挥手？

这是因为TCP连接的全双工通信，若客户端发送请求终止连接后，待服务端确认后，便可关闭客户端到服务端的TCP连接，此时处于半关闭状态。待服务端不再发送数据时，向客户端发送请求终止连接后，待客户端确认后，才关闭服务端到客户端的TCP连接，至此完全释放双方的TCP连接，处于完全关闭状态。

### 11. 两台计算机至今如何使用http协议进行通信？

两台计算机使用http协议进行通信，在一条通信线路上，一个作为客户端，另一个作为服务端，当客户端把请求封装成http请求报文发送给服务端，服务端接收到了请求后，组织响应数据封装成http响应报文返回给客户端。

### 12. HTTP请求报文格式。

HTTP请求报文由请求行、请求头、空行和请求体组成。

- 请求行包含请求协议、URI和协议版本。
- 请求头由多行键值对组成，每个键值对用冒号分开，用来补充传输的信息。
- 空行用来隔开请求头和请求体
- 请求体仅在向服务器提供参数时使用，比如POST请求。

```bash
GET /index.html HTTP/1.1
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.9
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.9,en;q=0.8
Cache-Control: max-age=0
Host: www.example.com
If-Modified-Since: Thu, 17 Oct 2019 07:18:26 GMT
If-None-Match: "3147526947+gzip"
Proxy-Connection: keep-alive
Upgrade-Insecure-Requests: 1
User-Agent: Mozilla/5.0 xxx

param1=1&param2=2
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

### 13. HTTP响应报文格式

一个HTTP响应报文通常由响应行、响应头、空行和响应体。

响应行包含协议版本、状态码、以及状态描述。

响应头包含多个键值对，用来补充响应的信息。

空行用来分隔响应头和响应体。

响应体为服务端向客户端发送的实际数据

```bash
HTTP/1.1 200 OK
Age: 529651
Cache-Control: max-age=604800
Connection: keep-alive
Content-Encoding: gzip
Content-Length: 648
Content-Type: text/html; charset=UTF-8
Date: Mon, 02 Nov 2020 17:53:39 GMT
Etag: "3147526947+ident+gzip"
Expires: Mon, 09 Nov 2020 17:53:39 GMT
Keep-Alive: timeout=4
Last-Modified: Thu, 17 Oct 2019 07:18:26 GMT
Proxy-Connection: keep-alive
Server: ECS (sjc/16DF)
Vary: Accept-Encoding
X-Cache: HIT

<!doctype html>
<html>
<head>
    <title>Example Domain</title>
	// 省略... 
</body>
</html>
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

### 14. HTTP请求方法知道哪些？

HTTP1.0定义了GET、POST和HEAD

HTTP1.1新增了PUT、PATCH、DELETE、CONNECT、OPTIONS、TRACE

- GET：请求资源，指定的资源经过服务端解析后返回响应内容
- POST：向指定的资源上传数据进行处理，数据包含在请求体当中
- HEAD：与GET类似，不过只返回报文首部，验证URI资源的有效性和资源更新时间。
- PUT：上传文件，但是不带有验证机制
- PATCH：允许对资源进行部分修改
- DELETE：与PUT功能相反，用于删除资源
- CONNECT：建立网络连接，通常用于SSL/TSL加密的代理服务器
- TRACE：用来返回客户端到服务端的路径
- OPTIONS：获取目标资源的请求方式

### 15. HTTP状态码

| 状态码 | 类别                             | 含义                         |
| ------ | -------------------------------- | ---------------------------- |
| 1xx    | （informational）信息性状态码    | 请求正在处理                 |
| 2xx    | （success）成功状态码            | 请求正常处理完毕             |
| 3xx    | （redirectional）重定向状态码    | 需要进行附加操作来完成后请求 |
| 4xx    | （Client Error）客户端错误状态码 | 服务端无法处理请求           |
| 5xx    | （Server Error）服务端错误状态码 | 服务端处理请求出错           |

- 1xx informational 信息性状态码 请求正在处理 
  - 100 Continue 到目前为止请求都正常，客户端可以继续发送请求或者忽略该响应报文
- 2xx success 成功状态码 请求正常处理 
  - 200 OK 请求处理成功
  - 204 No Content 请求处理成功，但是返回的响应报文不包含实体的主体内容
  - 206 Particial Content 客户端进行了范围请求，返回的响应报文为Content-Range指定范围内的内容
- 3xx redirectional 重定向状态码 需要执行附加操作来完成请求 
  - 301 Moved Permanently 永久性重定义
  - 302 Found 暂时重定向
  - 304 Not Modified 资源未被改，可以使用缓存版本
- 4xx Client Error 客户端错误状态码 服务端无法处理请求 
  - 400 Bad Request 请求报文存在语法错误
  - 401 Unauthorized 请求报文未校验，需要进行身份验证
  - 403 Forbidden 没有权限访问资源
  - 404 Not Found 没找到
- 5xx Server Error 服务端错误状态码 服务端处理报文出错 
  - 500 Internal Server Error 服务端内部出错
  - 503 Service Unavailable 服务端处于超负载/停机维护，无法处理请求。

### 16. HTTP1.0和HTTP1.1之间的区别

（1）缓存机制

HTTP1.0主要使用Headers里的Expires、Last_modified和If_Modified_Since字段实现缓存机制，具体的话：

- 首先服务端初次返回给客户端的响应体，会使用Last_Modified字段来标记被请求的资源在服务端的最后的修改时间，使用Expires字段来约定一个响应体的过期时间，若客户端的缓存资源过了Expires的过期时间，便会自动删除。
- 当客户端再次向服务端请求该资源时，在请求头中使用If_Modified_Since字段，If_Modified_Since的值就是上一次获得该资源响应体中Last_Modified值，服务端接收到了请求报文并判断If_Modified_Since时间后，资源确实没有修改，则会返回客户端一个304 Not_Modified 状态码的响应报文，表示可以直接从客户端的缓存资源里取。
- 若判断If_Modified_Since后，资源被修改过，则会返回一个状态码为200 OK的响应报文，响应体会附带全新的资源内容。

HTTP1.1的缓存机制的基本工作原理与HTTP1.0保持不变，只是添加了更多的缓存控制策略例如Entity tag、If_None_Match、Cache_Control等。

- Entity Tag是特定版本资源的不透明标识符，若资源遭到修改，则会重新分配一个新的Entity_Tag。
- 服务端初次发送给客户端的响应体，会在响应头中包含Entity_Tag字段。
- 当客户端再次发送请求时，请求头中添加If_None_Match字段，值就是之前Entity返回的内容，服务端判断发过来的If_None_Match的值和该资源计算出来的Entity值是否匹配，匹配就返回状态码为304 Not Modified 响应报文，否则返回200 OK 的响应报文，会附带全新的资源和新的Entity Tag。

（2）连接方式

HTTP/1.0 使用短连接，HTTP/1.1默认使用长连接

- HTTP短连接就是，客户端和服务端每进行一次HTTP请求，就会建立一次连接，任务结束后就会关闭连接，当客户端访问的html文件中包含其他的web资源，例如图像文件，每遇到一次这样的web资源，客户端便需要重新建立一次TCP连接。 
  - 客户端请求html文件，服务端发送html文件，客户端（浏览器）解析html语言，发现html文件中包含其他资源，那么客户端会对这些包含的资源再进行请求，由于是短连接，因此每次再次打开和关闭TCP连接。
  - 短连接会导致有大量的握手报文和挥手报文占用带宽（**带宽**（Bandwidth）是指在单位时间内传输数据的能力，通常用每秒传输的位数（bps，比特每秒）来表示）
- HTTP长连接就是请求报文中在请求头加入Connection:Keep-alive，这样TCP连接将持续打开，客户端再次访问这个服务端时会继续使用已经建立的TCP连接。

（3）流水线处理 （管道化Pipeline）

在HTTP/1.0中，每个请求都需要等待前一个请求的响应，而HTTP/1.1的长连接可以连续地发出请求，不用再等待响应后再发送

（4）状态码

HTTP/1.1增加了大量的状态码

（5）Host头处理

HTTP/1.1引入了HOST头部字段，支持虚拟主机（域名解析DNS支持多个域名绑定到同一个IP地址上）

（6）带宽优化

HTTP/1.1引入了范围请求机制，允许请求资源的一部分，返回状态码为206 particial Content，以避免带宽的浪费

### 17. HTTP不安全性体现在哪些

- 通信的数据使用明文，容易被窃听 
  - 例子：拦截数据包，可以看到HTTP发送的明文数据
- 不验证通信对方的身份，容易被伪装 
  - A与B进行通信，C可以冒充B/A，通过发送自己的公钥，然后用自己的私钥解密。
- 无法验证通信内容的完整性，容易被篡改 
  - 可以修改通信的内容

### 18. 非对称加密和对称加密

非对称加密：

通信的双方（客户端/服务端）都准备自己的一对公钥和私钥，而公钥是公开的。因此通信一方都可以使用通信的另一方的公钥进行加密通信内容，通信的另一方就可以使用自己的私钥进行解密。

对称加密：

通信双发共享一密钥，加密和解密方式公开，加密方使用密钥进行加密，解密方使用密钥进行解密即可。

### 19. 数字证书和数字签名

数字证书是为了验证双方的身份，而数字签名则是为了防止证书本身在传输的过程中被篡改。

具体的流程如下：

（1）服务端申请数字证书

- CA拥有一对公钥和私钥，服务端向网站申请数字证书。
- CA首先对服务端的公钥进行Hash得到摘录信息。
- 然后使用自己的私钥对摘录信息进行加密，继而得到数字签名。
- CA将数字签名和服务端的公开密钥放入数字证书发送给服务端。

（2）客户端验证数字证书

- 客户端使用CA的公钥对数字签名进行解密得到摘录信息1
- 再对数字证书中服务端的公钥进行Hash算法得到摘录信息2
- 比较摘录信息1和摘录信息2，相等，则服务端的公钥有效。

### 20. 为什么SSL/TLS不使用非对称加密？

SSL/TLS使用混合加密方式：TLS/SSL协议使用非对称加密算法来进行共享密钥的交换，然后再使用共享密钥通过对称加密的方式进行加密数据传输。

这是因为非对称加密数据比对称加密数据，花费的时间巨大，系统消耗也巨大，而使用混合加密的方式，既可以利用非对称加密的安全性，又可以利用对称加密的速度快的优点。

### 21. TCP如何保证可靠传输？

- 序列号和确认应答：每个TCP报文段都有一个序列号seq，接受方会回传一个确认号ack，表示期望收到下一次报文的序列号，这样发送方知道哪些报文段被接收，哪些需要重传。
- 数据校验：TCP使用数据校验和来检测数据在传输过程中是否发生损坏。发送方计算数据校验和并将其添加到TCP报文段的首部中，接收方收到报文段也计算数据校验和，与报文段中首部中的校验和进行比较，若不一致，则要求重传。（TCP数据校验不能绝对保证数据的正确，因为可能发生多个比特发生改变，而最后的数据校验和不变）。
- 超时重传：如果发送方在一定的时间（定时器）内未收到接收方对特定报文段的确认，则会认为该报文段丢失，进行重传。
- 流量控制：TCP使用滑动窗口机制实现流量控制，接受方通过使用窗口大小字段（Window Size）来告知发送方自己缓存区的大小，发送方根据窗口大小来控制自己发送数据的速度。
- 拥塞控制：TCP维持一个拥塞窗口（cwnd）和一个慢开始门限ssthresh的状态变量，使用四种算法来进行拥塞控制，即慢开始、拥塞避免、快重传和快恢复。 
  - 慢开始指的是，cwnd初始值为1，每经过一个往返时间，cwnd翻倍
  - 拥塞避免指的是：当cnwd大于等于慢开始门限ssthresh，拥塞窗口cwnd，每经过一个往返时间，cwnd值增加1.
  - 快重传：接收方每接到一个不按照顺序的报文段，便会发送一次确认，当发送方接收到了三次该序号的确认，发送方不会等待超时，而是立即重传这个丢失的报文段。
  - 快恢复，快恢复是基于快重传的，当发送方接收到了三次相同的确认报文段，除了立即重传该丢失的报文段外，还将拥塞窗口cwnd减半，然后进入到快恢复，每一个往返时间，增加一。

### 22. TCP的粘包和拆包

因为TCP是面向字节流的传输协议，数据被视为一连串的字节流，数据的边界在传输过程中是不可见的。

TCP在发送数据时，会通过缓冲区来进行优化

- 粘包 
  - 当待发送的数据小于TCP发送缓冲区的大小，TCP会将发送缓冲区的数据报合并为一次发送
  - 当接收端的应用层没有及时读取接收缓冲区中的数据，将发生粘包
- 拆包 
  - 待发送的数据大于发送缓冲区的数据，将会拆分为多次发送。

如何解决？

- TCP首部添加一个表示后续数据长度的字段，接收方通过这个字段长度值，从而判断数据报的边界
- 在每个数据包的末尾采用特殊的分隔符，例如FTP协议
- 每个数据包固定长度

### 23. DNS完整域名解析过程

- 首先查询电脑中缓存的域名（hosts文件），若没有则向本地DNS服务器查询
- 本地DNS服务器查找域名并无记录，则向根DNS服务器发送请求
- 跟服务器注意到域名中包含顶级域名（edu、com、cn）后，则向本地DNS服务器返回其包含的顶级域DNS服务器
- 本地DNS服务器向顶级域服务器发送请求，询问IP地址，顶级域服务器仍不知道请求域名的IP地址，但是其观察到该域名中包含（baidu.com,xxx.edu）权威域名，因此返回权威域服务器的地址
- 00本地DNS服务器向权威域服务器发送请求，请求的域名在权威域DNS服务器（权威DNS服务器是负责存储特定域名下所有主机记录）备过案，因此将其IP地址返回给本地DNS服务器。
- 本地DNS服务器将目标域名的IP地址返回给请求主机。

客户端和本地域名服务器使用的是递归查询，而其他的使用迭代查询，主要原因在于防止跟服务器的压力过大。

### 24. DNS负载均衡

DNS负载均衡，是通过DNS协议来分配网络流量和负载的技术。目的是将请求均匀地分散到多个服务器上，以避免单一服务器过载。

它的原理就是在DNS服务器中为同一个域名配置多个IP地址，在应答DNS查询时，DNS服务器会按照负载均衡的策略（例如基于轮询、基于权重、基于地理位置）将这些IP地址按顺序分配给客户端。

### 25.OSI七层模型

- 物理层 
  - 负责传输原始的比特流，将数据转换为比特流发送到物理介质上，以及从物理介质上接收比特流转化成数据，它主要关注传输媒介、数据的传输速率等
- 数据链路层 
  - 数据链路层怎么进行传输数据？
    - 封装数据帧：数据链路层将从上层接收到的数据包（IP数据包）封装成数据帧，数据帧是数据链路层传输的最小数据单位（包括数据、帧首部、帧尾部）
    - 添加帧头部和帧尾部，数据链路层在数据包的前后添加帧首部和帧尾部，帧首部包含目标MAC地址和源MAC地址，帧尾部则一般包含一些错误检测信息，例如循环冗余校验码CRC，用于在接收端检测数据传输过程中是否出错。
    - 发送数据帧：封装完成的数据帧会被发送到物理层，通过物理层传输到目标设备
    - 接收数据帧，在目标设备上，数据链路层接收到了传输过来的数据帧，会根据帧首部的目标MAC地址判断是否属于自己的数据帧
    - 提取数据，数据链路层接收到了自己的数据帧之后，会提取其中的数据上传了上一层
- 网络层 
  - 负责通过路由选择算法，实现数据包的寻址、路由和转发
- 传输层 
  - 负责提供端到端的数据传输
- 会话层 
  - 负责建立、管理和终止会话
- 表示层 
  - 负责数据的编码和解码，实现不同计算机系统之间的数据格式转换和数据压缩
- 应用层 
  - 负责为用户提供接口和服务

### 26. TCP/IP 四层模型

- 应用层 
  - 应用层位于传输层之上，主要提供两个终端设备上应用程序之间的沟通，它定义了信息交换的格式。我们把应用层交互的数据单元称为报文
- 传输层 
  - 传输层负责向两个终端设备进程之间提供通用的数据传输服务
- 网络层 
  - 网络层为分组交换网上的不同主机提供通信服务，在发送数据时，网络层把运输层产生的报文段或用户数据报封装成分组和包进行传送。在 TCP/IP 体系结构中，由于网络层使用 IP 协议，因此分组也叫 IP 数据报，简称数据报。⚠️ 注意：**不要把运输层的“用户数据报 UDP”和网络层的“IP 数据报”弄混**。
  - 网络层的另一个目的是听过路由选择算法，实现数据报的寻址、路由和转发
- 网络接口层 
  - 我们可以把网络接口层看作是数据链路层和物理层的合体。
  - 数据链路层负责将网络层交下来的IP数据报封装成帧，在两个相邻节点之间的链路上传输帧
  - 物理层则是实现相邻节点之间的比特流透明传输，尽可能屏蔽吊具体传输介质和物理设备的差异。

### 27. IP协议

IP协议网际协议

### 28. ARP

地址解析协议，它解决的是网络层地址和链路层地址之间的转换问题，因为一个IP数据报在物理上进行传输的过程，总是需要下一跳（物理上的下一个目的），而IP属于逻辑地址，mac地址才是物理地址，ARP地址解析协议解决了IP地址转MAC地址的问题。

ARP的工作原理：三个关键词：ARP表、广播问询、单播响应。

在每一个局域网，每个网络设备都自己维护了一个ARP表，ARP表记录了某些其他网络设备的IP地址与MAC地址映射的关系，该映射关系以<IP,MAC,TTL> 三元组组成，TTL为该映射关系的生存周期，一般为20分钟。

ARP的工作原理将分成两种场景进行讨论：

- 同一个局域网内的MAC寻址
  - 假设主机A向同一局域网下的主机B发送IP数据报文，主机A检索自己的ARP表，发现ARP表中并无主机B的IP地址所对应的映射，因此不知道主机B的MAC地址，若是在ARP表中查询到了主机B的映射记录，那么只需提取MAC地址并构造链路层数据帧发送即可。
  - 主机A将构造一个ARP查询分组，并将其广播道所在的局域网中。
    - ARP分组是一种特殊的报文，ARP分组有两种，一种是查询分组，另外一个便是响应分组。
  - 主机B收到了主机A广播的查询分组后，知道是对自己的闻讯，接着构造出了以一个ARP响应分组，同时，主机B根据ARP查询分组的IP和MAC地址在自己的ARP表中添加一条映射记录。
  - 主机A收到主机B的响应分组后，提取其中的IP地址和MAC地址后，在自己的ARP表中添加一条主机B IP与MAC地址的映射记录。
- 从一个局域网到另一个局域网中网络设备的寻址





### TCP 字段



\30. cookie和session的区别

## 二、C++

### 1. C++中指针和引用的区别

- 指针是一个变量，其值是指向变量的地址，而引用是一个别名，是一个已存在变量的别名。
- 指针可以被重新赋值指向不同的内存地址（也可以为空指针nullptr），并且指针不用初始化；而引用必须在定义时被初始化（引用也不能为空，NULL），且不能被重新赋值指向其他变量。
- 指针可以为多级，引用只有一级
- sizeof 指针得到的是该指针的大小（32位的话为4字节，64位的话为8字节），而sizeof 引用则是被引用对象的大小
- 作为参数传递时，需要使用指针操作符*来间接修改指向的对象，而引用可以直接对其指向的对象修改。

### 1. C++中NULL和nullptr

C++引入nullptr是为了更好的类型安全，因为在C++中NULL通常被定义为整数0，而当出现函数重载时，函数的参数一个为指针，另一个为整数，此时使用NULL作为参数就会出现函数的二义性。nullptr是一种特定的指针类型，可以明确区分整数和指针类型，避免了函数重载时的二义性，因此使用nullptr定义空指针，以获得更好的类型安全。

### 2. sizeof

操作系统32位和处理器64位这是两个不同的概念。

sizeof是C语言中的运算符，用来计算一个类型/变量/对象的字节大小。

通常计算掌握几个技巧：

- 指针的大小取决于处理器位数，32位就是4字节，64位就是8字节
- 数组 = 基本类型大小（short 2字节 char 1字节 int/float 4字节 double 8字节）* 数组大小
- 字符串数组要算上末尾的 '\0’
- 数组作为函数参数时会退化成指针
- struct 结构体要考虑字节对齐，这与操作系统位数有关，结构体的大小通常会被向上取整到其最大成员的大小的倍数

```cpp
#include <iostream>
#include <cstdlib>
void func(int* temp){
    std::cout << sizeof(temp) << std::endl;
}

// 操作系统32位（4字节），这与字节对齐有关
struct S1 {
    char a;   // 本来1字节，padding 3 字节
    int b;    //  4 字节
    short c;  // 本来 short 2字节，但是整体需要按照 4 字节对齐(成员对齐边界最大的是int 4) ，
    //所以需要padding 5，总共: 1 + 3（padding） + 4 + 2 + 2（padding）
};
//
struct S2 {
    // char 1字节、short 2字节 因此可以先补充1字节padding后，short两字节就可以在其类型大小的整数倍上
    char a;
    short c;
    int b;    //  4 字节
    //所以需要padding 1，总共: 1 + 1 + 2 + 4
};
// 1+2+2+2+1
struct MyStruct3 {
 char a;
 short b;
 short c;
 short d;
 char e;
};
struct MyStruct {
 double a;    // 8 个字节
 char b;      // 本来占一个字节，但是接下来的 int 需要起始地址为4的倍数
              //所以这里也会加3字节的padding
 int c;       // 4 个字节

 // 总共:  8 + 4 + 4 = 16
};
struct MyStruct1 {
 char b;    // 本来1个字节 + 7个字节padding
 double a;  // 8 个字节
 short c;     // 本来 2 个字节，但是整体要按最大成员double字节对齐，所以 6个字节padding
  // 总共: 8 + 8 + 8 = 24
};

int main() {
    int arr1[10];
    double arr2[10];
    char arr3[] = "HELLO";
    std::cout << sizeof(arr1) << std::endl;// 40 4*10
    std::cout << sizeof(arr2) << std::endl;// 80 8*10
    std::cout << sizeof(arr3) << std::endl;// 6 字符串要算上末尾的'\0'(空字符通常用来表示字符串的结束)

    func(arr1);// 数组作为函数参数会退化为指针，答案为8

    int* a = static_cast<int*>(std::malloc(10)); // 分配10个整数的内存空间，并将返回的void*指针转换为int*类型
    std::cout << sizeof(a) << std::endl; // 你申请的内存大小，而你本身指针的大小为8，并不冲突
    std::free(a); // 释放通过malloc分配的内存

    // 字节对齐
    std::cout << sizeof(S1) << std::endl;// 12
    std::cout << sizeof(S2) << std::endl;// 8
    std::cout << sizeof(MyStruct) << std::endl;// 16
    std::cout << sizeof(MyStruct1) << std::endl;// 24
    std::cout << sizeof(MyStruct3) << std::endl;// 10 //结构体的大小被向上取整到最大成员short2的倍数
    return 0;
}
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

### 3. 字节对齐/内存对齐

- 内存分配的顺序是按照声明的顺序

- 每个变量相对于内存的初始地址的偏移量必须是该变量类型大小的整数倍(若内存的初始地址为0，一个 `int` 类型通常是4字节，那么该变量的起始地址就为0 4 8 12....)

- 整个结构体的内存对其方式按照结构体内变量类型最大来对齐，即该结构体的大小要是最大变量类型的整数倍。 

  ```cpp
  // 我们假设内存初始地址为0 
  struct MyStruct {
      char a;   // 1字节 其按照1字节对齐，即起始地址为1的倍数（起始地址-内存初始地址为0）
      int b;    // 4字节（通常） 其按照1字节对齐，即起始地址为4的倍数（起始地址-内存初始地址为0）因此需要补齐3个字节，在地址4上存储
      double c; // 8字节（通常）正好地址为8，是double类型的倍数，直接存储
      char d; 直接存储
  };
  // 但是最后整个结构体的大小要是最大类型的倍数。因此补齐7个字节变成24字节（8*3）。
  ```

  ![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

- 也可以自己定义对齐方式#pragma pack(n)

### 4. C和C++的区别

- 面向过程与面向对象：C语言是面向过程的语言，考虑的是如何通过一个过程对输入进行处理得到输出；C++是面向对象的语言，主要的特征就是封装、继承和多态。封装是隐藏类内部的属性以及方法的实现细节，仅暴露一些必要的接口，使得代码模块化；继承是创建共享代码的层次性结构，派生类可以复用基类的代码，也可以对基类的方法进行扩展，提高了代码的复用性和可扩展性；多态则是不同的类对象，调用相同的接口却产生不同的效果。
- 内存管理：在C语言中使用malloc()和free()来进行内存分配和释放，在C++中使用new和delete操作符进行内存分配和释放，另外C++11中引进了智能指针，提供了更安全和方便的内存管理方式
- C++引入了引用的概念。

### 5. 智能指针的原理、常用的智能指针及实现

原理：智能指针是C++中用于管理动态分配内存的类，通过在对象的构造函数中分配内存，并在析构函数中释放内存，使用引用计数技术来追踪指向动态分配内存的引用数，当引用计数的值为零时，智能指针会自动地释放内存。

常用的智能指针：

- std::shared_ptr 

  - 第一次创建类的新对象时，动态分配内存，智能指针初始化，指向该对象，并将该对象的引用计数值初始化为1。

  - 使用拷贝构造函数的方式创建一个新的std::shared_ptr副本时，两shared_ptr指向相同的对象，增加一次该对象的引用计数值。

  - 使用赋值运算符方式，用一个std::shared_ptr赋值给另一个std::shared_ptr时，赋值运算符重载会将左操作数所指对象的引用计数减1，右操作数所指的对象的引用计数值加一。并对左操作数所指的对象的引用计数进行判断，若为0，则意味着没有智能指针引用该对象，该对象进行销毁，内存释放。

  - 当每一个shared_ptr被销毁时（例如超出了其作用域），调用其析构函数，析构函数对该对象的引用计数值减一，当引用计数值为0时，调用该对象的虚构函数，进行指向对象内存的释放。

  - shared_ptr常见操作： 	

    ```cpp
    make_shared<T>(args) // 返回一个shared_ptr，指向一个动态分配的类型为T的对象。使用args初始化此对象
    shared_ptr<T> p(q) // p是shared_ptr q的拷贝；此操作会递增q中的引用计数。q中的指针必须能转换成T*
    p = q // p和q都是shared_ptr，所保存的指针必须能相互转换。此操作会递减p中的引用计数，递增q中的引用计数。若p中的引用计数变为0，则将其管理的原内存释放
    p.unique() // 若p.use_count()为1，返回true；否则返回false
    p.use_count() // 返回与p共享对象的智能指针数量；可能很慢，主要用于调试
    ```

    ![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

- std::weak_ptr 

  - 引入std::weak_ptr的原因：std::weak_ptr是为了shared_ptr循环引用的死锁问题（我们假设有A和B两个类，创建共享指针shared_ptr1指向A，创建共享指针shared_ptr2指向B，而A对象和B对象均有类成员变量共享指针类型，我们分别让其指向对方的类对象。此时形成相互的引用计数，在最后析构时，先调用A对象的析构函数，再调用B对象的析构函数，当

    ```
    a
    ```

    和

    ```
    b
    ```

    变量超出作用域时，它们的析构函数会被调用。这将导致A对象和B对象的引用计数各自减1。然而，由于A对象的成员变量

    ```
    b_ptr
    ```

    仍然持有对B对象的引用（你假设可以b_ptr可以析构了，那么B对象这块内存就被释放了，但是B对象这块内存中还有a_ptr指向A对象的shared_ptr指针，因此无法析构），且B对象的成员变量

    ```
    a_ptr
    ```

    仍然持有对A对象的引用，所以它们的引用计数都为1）。 	

    ```cpp
    #include <iostream>
    #include <memory>
    
    class Node {
    public:
        std::shared_ptr<Node> next;
    
        Node() {
            std::cout << "Node Constructor" << std::endl;
        }
    
        ~Node() {
            std::cout << "Node Destructor" << std::endl;
        }
    };
    
    int main() {
        std::shared_ptr<Node> node1 = std::make_shared<Node>();
        std::shared_ptr<Node> node2 = std::make_shared<Node>();
    
        // 形成循环引用
        node1->next = node2; // node1 引用计数 1 node2 引用计数为2
        node2->next = node1; // node1 引用计数 2 node2 引用计数为2
    
        // node1 和 node2 的引用计数永远不会降至0，导致内存泄漏
        return 0;
    }
    
    // 出了函数作用域，node2 共享指针先析构，node1共享指针再析构
    // 析构完 
    ```

    ![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

  - 使用weak_ptr就可以解决循环引用的问题，weak_ptr指向shared_ptr指向的资源，但是并不会增加该资源的引用计数值，weak_ptr只具有观测权，并不能共享指针（因此weak_ptr并没有重载operator*和->操作符）。

  - weak_ptr常见操作： 	

    ```cpp
    weak_ptr<T> w;	// 空weak_ptr可以指向类型为T的对象
    weak_ptr<T> w(shared_ptr p);	// 与p指向相同对象的weak_ptr, T必须能转换为sp指向的类型
    w = p;	// p可以是shared_ptr或者weak_ptr，赋值后w和p共享对象
    w.reset();	// weak_ptr置为空
    w.use_count();	// 与w共享对象的shared_ptr的计数
    w.expired();	// w.use_count()为0则返回true，否则返回false
    w.lock();	// w.expired()为true，返回空的shared_ptr;否则返回指向w的shared_ptr
    ```

    ![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

- unique_ptr独占的智能指针 

  - unique_ptr与shared_ptr使用方法差不多，但是功能更为单一，它保证指向的内存只能由一个unique_ptr拥有（更像原生的指针，但是能够自己自动释放）不允许赋值和拷贝操作，只允许移动。

### 6. 循环引用

在C++shared_ptr共享智能指针中，两个shared_ptr初始化类对象A和类对象B，然后类对象A与类对象B中均有shared_ptr指针指向另一方对象，形成相互引用。这样导致它们的引用次数不会降为零，因而无法释放内存，导致内存泄漏。

### 7. 讲一讲你对lambda表达式的理解

- lambda作用：首先利用lambda表达式可以编写内嵌的匿名函数，用来替换独立函数以及函数对象。
- lambda组成：lambda的语法形式由  [捕获列表](参数列表) mutable(optional) ->函数返回类型{lambda函数题} 构成。其中的捕获列表分为[]：不捕获外部变量；[a]按值捕获外部变量；[&]按引用捕获外部变量。 mutable关键字 指的是可以在lambda函数体内部作用域修改其捕获的外部变量值。
- 编译器如何看待lambda表达式：当编译器遇到lambda表达式，会自动生成一个匿名类，会使用lambda表达式的捕获列表、参数列表以及函数体对匿名类进行定义以及operator运算符的重载，称之为闭包类型。在运行时，lambda表达式，返回一个匿名的闭包实例，这个闭包对象可以像普通函数那样调用。

```cpp
#include <cstdio>
#include <algorithm>
#include <vector>
using namespace std;
int cmp(int a,int b){
    return a<b;
}
int main(){
    vector<int> v = {5,4,3,2,1};
    // 编写内嵌的匿名函数
    sort(v.begin(),v.end(),[](int a,int b){return a<b;});
    sort(v.begin(),v.end(),cmp);//两者等价
    return 0;
}
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

如何对匿名类定义以及operator运算符重载：

- lambda表达式捕获列表[]用来匿名类构造函数的参数传递
- lambda表达式中的(函数参数)用来重载匿名类的operator()(函数参数)的重载。

```cpp
#include <iostream>

// 编译器生成的匿名闭包类（简化版本）
class AnonymousClosure {
    int captured_x; // 按值捕获的变量x的副本
    int& captured_y; // 按引用捕获的变量y的引用

public:
    AnonymousClosure(int x, int& y) : captured_x(x), captured_y(y) {}

    void operator()(int a,int b) const {
        std::cout << "Captured x: " << captured_x << std::endl;
        std::cout << "Captured y by reference: " << captured_y << std::endl;
        std::cout << "参数列表"<< a <<" "<< b << std::endl;
    }
};

// lambda对象的实例化
int main() {
    int x = 10;
    int y = 20;
    auto lambda = [x,&y](int a,int b){
    std::cout << "Captured x: " << x << std::endl; // 按值捕获x
    std::cout << "Captured y by reference: " << y << std::endl; // 按引用捕获y
    std::cout << "参数列表"<< a <<" "<< b << std::endl;
    };
    AnonymousClosure closure(x, y); // 创建匿名闭包类的实例
    closure(1,2); //函数重载
    lambda(1,2); // 像普通函数一样调用
    return 0;
}
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

### 8. 讲一下c++程序的内存分区/内存模型

- 栈：当执行函数时，函数的参数以及局部变量都会存储在栈上，当执行结束后，这些存储单元会被释放。栈的内存分配内置于处理器的指令集当中，因此效率高，但是栈的内存容量并不大。
- 堆：是在c++中使用new或者c语言中使用malloc分配的内存块，这些内存的分配以及释放需要程序员手动去操作，使用delete或者free去释放内存。
- 全局/静态存储区：存储全局变量和静态变量，这些内存在程序整个运行期间都存在。
- 常量区：存储常量，不允许修改
- 代码区：存储函数体的二进制代码

### 9. new和delete是如何实现的？

new和delete是C++的操作符：

new操作符：

- 分配内存空间，new 首先调用operator new(size)函数，用于分配指定大小的内存块
- 调用构造函数：若new的类型是一个对象，那么new操作符还会调用对象的构造函数，进行初始化类对象。
- 返回指针：new操作符最终返回分配内存的指针。

delete操作符：

- 调用析构函数，如果delete删除的是类对象，那么则会调用类对象的析构函数
- 释放内存空间：delete调用operator delete(void* ptr)函数，释放先前分配的指针。

### 10. new和delete 与 malloc和free有什么区别？

- new和delele在为类对象申请内存时，除了申请内存之外，还会调用类的构造函数和析构函数。
- 使用new操作符申请内存时无需制定内存块的大小，编译器会根据类型信息自行计算，而malloc则需要显示地指出所需内存的大小
- new操作符内存申请成功后，返回的是对象类型的指针，类型严格与对象匹配，因此new是类型安全的，而malloc返回的是void*，需要通过类型转换为我们需要的格式。

### 11. 面向对象的三大特性

- 封装：封装是指将数据（属性）和方法组合成一个类（class）的过程。 
  - 封装的主要目的是隐藏类内部的数据和方法实现细节，只暴露一些必要的接口。
  - 可以通过控制访问类成员的权限（public、private、protected）限制对类成员的访问，从而保证数据的安全性。
- 继承：继承是指派生类继承基类的属性和方法的过程。 
  - 继承可以创建具有共享代码的类层次结构，派生类可以复用基类的代码，也可以对基类的代码进行扩展，提高代码的复用性和可扩展性。
- 多态：多态是指不同的类对象调用相同的函数，表现出不同的行为。 
  - 多态分为运行时多态（也称动态多态）和编译时多态（静态多态），c++中使用虚函数和重写实现运行时多态，使用模板函数和重载实现编译时多态。
  - 虚函数是指在基类中声明的函数，派生类可以进行重写。运行时多态指的是基类的指针/引用指向派生类的对象，通过虚函数机制，调用到派生类重写的函数。
  - 模板函数，指的是编写通用型的代码，用于处理不同类型的数据
  - 重载：指的是，相同的函数名，但是函数参数不同，从而实现多态。

```cpp
#include <iostream>
#include <cstring>
using namespace std;
//Person类
class Person
{
public:
    Person(string name, int age):m_name(name),m_age(age){}
	virtual void info()
	{
		cout << "Call Person info, Name = " << this->m_name << " Age = " << this->m_age << endl;
	}
protected:
    string m_name;
    int m_age;
};
class Student:public Person
{
public:
    Student(string name, int age, float score):Person(name, age),m_score(score){}
	virtual void info()
	{
		cout << "Call Student info, Name = " << this->m_name << " Age = " << this->m_age << " Score = " << m_score << endl;
	}
protected:
    float m_score;
};
int main()
{
    // 引用实现多态
	Person person("Base", 18);
	Student student("Derived", 20, 110);
	Person &rPerson = person;
    Person &rStudent = student;
    rPerson.info();
    rStudent.info();
    
    // 指针实现多态
    Person* person1 = nullptr;
	person1 =  new Student("Derived", 20, 110);
    person1->info();
    delete person1;
	return 0;
}
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

![img](https://img-blog.csdnimg.cn/f2238f16891442c5ae34913ba69646fe.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)编辑

### 12. 继承常见知识

派生类继承基类，派生类会继承基类的所有属性和方法，但是基类成员在派生类的访问权限收到继承方式的影响。

- public继承 

  - | 基类成员访问权限 | 在派生类访问权限 |
    | ---------------- | ---------------- |
    | public           | public           |
    | protected        | protected        |
    | private          | 不可访问         |

- protected继承

  - | 基类成员访问权限 | 在派生类访问权限 |
    | ---------------- | ---------------- |
    | public           | protected        |
    | protected        | protected        |
    | private          | 不可访问         |

- private继承 

  - | 基类成员访问权限 | 在派生类访问权限 |
    | ---------------- | ---------------- |
    | public           | private          |
    | protected        | private          |
    | private          | 不可访问         |

 c++构造函数调用顺序：

- 定义派生类构造函数可以指明基类构造函数，若不指明，则会默认地调用基类的构造函数（不带参的构造函数，若基类只有自定义参数的构造函数，那么则会没有默认的构造函数，则会编译失败）。

```cpp
#include <cstdio>

class Base{
private:
    int a;
    int b;
public:
    // 自定义带参构造函数
    // 可以使用初始化列表
    Base(int _a,int _b):a(_a),b(_b){
        printf("This is Base\n");
    }
    Base(){
        printf("This is Base\n");
    }
};
class Derived1:public Base{
private:
    int c;
public:
    Derived1(int _a,int _b,int _c):Base(_a,_b),c(_c){
        printf("This is Derived1\n");
    }
    Derived1(){
        printf("This is Derived1\n");
    }
};
int main(){
    Derived1 d1;
    Derived1 d2(1,2,3);
    return 0;

}
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

 ![img](https://img-blog.csdnimg.cn/54e41ed02a8e4efc9e8de0ab19807ca6.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)编辑

### 13. c++如何创建类对象

- 默认构造函数创建对象

```cpp
class MyClass {
public:
    MyClass() {
        // 默认构造函数
    }
};

int main() {
    MyClass obj; // 创建 MyClass 对象
    return 0;
}
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

- 带参数的构造函数创建对象

```cpp
class MyClass {
public:
    MyClass(int value) {
        // 带参数的构造函数
    }
};

int main() {
    MyClass obj(42); // 创建 MyClass 对象，调用带参数的构造函数
    return 0;
}
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

- 动态分配内存创建对象（在对上创建对象）：使用new在堆内存上动态分配创建对象，在使用结束后需要使用delete释放内存。

```cpp
class MyClass {
public:
    MyClass() {
        // 默认构造函数
    }
};

int main() {
    MyClass* objPtr = new MyClass(); // 动态分配内存创建 MyClass 对象
    // 使用 objPtr 操作对象
    delete objPtr; // 释放内存
    return 0;
}
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

### 14. 深拷贝与浅拷贝的区别

一个类拥有资源，当这个类的对象发生复制的时候，深拷贝就是会为资源重新分配独立的内存空间，而浅拷贝中多个对象会共享同一块内存。（比如类成员是指针类型）。

浅拷贝容易发生悬空指针，然后出现内存泄漏的问题。

类中有指针这样的成员属性，当使用一个对象副本对另一个对象实施浅拷贝后，两个对象会共享一个相同的指针。当其中一个对象调用析构函数时，会释放该指针的内存，而另一个对象还在使用这个指针，就会发生悬空指针的问题（因为它指向的内存已经释放）。

于是当另一个对象也销毁时，也动态释放了该指针的内存，然而该指针已经被释放了。

### 15. 虚函数是什么以及虚函数是如何实现的？

在C++中，虚函数是指基类中声明的函数，用关键字virtual进行标识，这样的函数可以在派生类中进行重写，当使用基类指针/引用指向派生类对象时，虚函数会判断对象实际的类型来调用相应的函数。

虚函数是通过虚函数表实现的，每个声明了虚函数的类都会有一个虚函数表，其中存储了指向实际函数的地址，当派生类会继承基类的虚函数表，并且当派生类重写虚函数时，会更新该类虚函数中相应函数的地址。

### 16. 为什么析构函数一般写成虚函数？

由于类的多态性，我们可以使用基类指针指向派生类的对象，如果删除该基类指针，就会调用该指针指向的析构函数，将析构函数若是虚函数，则会指向派生类的析构函数，而派生类的析构函数又会自动调用基类的析构函数，这样整个派生类的对象被完全释放。

若不声明为虚函数，则编译器实施静态绑定，在删除基类指针的话，指挥调用基类的析构函数而不调用派生类的析构函数，从而派生类的对象析构不完全，造成内存泄漏。

```cpp
#include <cstdio>

using namespace std;


class Base{
public:
    virtual ~Base(){
        printf("Base 析构\n");
    }

};
class derived:public Base{
public:
    ~derived(){
        printf("derived 析构\n");
    }
};
int main(){
    Base* d = new derived();
    delete d;
    d = nullptr;
    // 析构函数加上virtual声明
    //derived 析构
    //Base 析构
    // 不加上
    //Base 析构  
    return 0;
}
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

### 17. 带有类成员变量的类对象构造函数和析构函数顺序？

- 构造时先调用类成员对象的构造函数（与声明的顺序有关），再调用类对象的构造函数。
- 析构时先调用类对象的析构函数，再按照相反声明的顺序，调用各自类成员对象的析构函数。
- 若是有继承关系，则先调用基类的构造函数（基类若有类成员变量则按照上述的构造顺序构造）。

```cpp
#include <iostream>
class Member {
public:
    Member() {
        std::cout << "Member Constructor" << std::endl;
    }

    ~Member() {
        std::cout << "Member Destructor" << std::endl;
    }
};

class Base {
public:
    Base() {
        std::cout << "Base Constructor" << std::endl;
    }

    virtual ~Base() {
        std::cout << "Base Destructor" << std::endl;
    }

private:
    Member member;
};

class Derived : public Base {
public:
    Derived() {
        std::cout << "Derived Constructor" << std::endl;
    }

    ~Derived() {
        std::cout << "Derived Destructor" << std::endl;
    }
};

int main() {
    Derived derived;
    return 0;
}
```

![img](https://img-blog.csdnimg.cn/4a6de028da5043deba3f58424392e529.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

### 18. new的用法

```cpp
#include <cstdio>
class MyClass {
public:
    MyClass(int value) : data(value) {
        // 带参数的构造函数，用于初始化对象
    }
    MyClass(){
        // 带参数的构造函数，用于初始化对象
    }
    MyClass(int value1,int value2):data(value1),data1(value2){
    }

    // 其他成员函数和数据成员可以在这里定义
    void print1(){
        printf("%d %d\n",data,data1);
    }


private:
    int data;
    int data1;
};

int main() {
    int size = 5; // 数组大小

    // 使用new关键字可以在堆内存上动态分配单个对象,不赋值
    int* a = new int();    // 等价于 int* a = new int;
    (*a) = 1;

    printf("%d\n",*a);

    // 使用new关键字可以在堆内存上动态分配单个对象,赋值
    int* b = new int(1);

    // new还可以用于动态分配数组
    int* arr = new int[size];
    for (int i = 0; i < size; ++i) {
        arr[i] = i;
    }

    // 动态分配多维数组
    int rows = 3;
    int cols = 4;
    int** matrix = new int*[rows];
    for (int i = 0; i < rows; ++i) {
        matrix[i] = new int[cols];
        for (int j = 0; j < cols; ++j) {
            matrix[i][j] = i * cols + j;
        }
    }

    // 动态分配 MyClass 对象并调用默认的构造函数
    MyClass* obj1 = new MyClass();
    // 动态分配 MyClass 对象并调用带参的构造函数
    MyClass* obj2 = new MyClass(2);
    obj2->print1();
    MyClass* objArray1 = new MyClass[size]{1,2,3,4,5};
    MyClass* objArray2 = new MyClass[size]{{1,1},{1,2},{1,3},{1,4},{1,5}}; // 动态分配 MyClass 对象数组并调用带参数的构造函数

    // 使用 objArray 操作对象数组
    // ...
    (objArray2+1)->print1();
    delete obj1;
    delete obj2;
    delete[] objArray1; // 释放内存，注意要使用 delete[] 来释放对象数组
    delete[] objArray2; // 释放内存，注意要使用 delete[] 来释放对象数组
    return 0;
}
```

### 19. 拷贝构造函数的使用场景

- 用类的一个对象去初始化另一个对象

- 当函数的参数是类时，也就是值传递的时候，如果是引用传递则不会

  - ```c++
    void getVector(Vector a){}
    Vector b;
    getVector(b);
    // 此时我们看 值传递其实完整来看就是Vector a = b;
    // C++中Vector a(b); 和 Vector a = b;是等价的 都是调用了Vector类的拷贝构造函数，只不过Vector a(b)是直接调用拷贝函数，而Vector a = b;使用了赋值初始化的语法。
    // 注意赋值运算符只有在初始化时才是调用拷贝构造函数，已经定义了后a = b只是将右侧对象的值（内容）赋给左侧对象。
    ```

- 当函数的返回值是类的对象或者引用时，也会调用拷贝构造函数

  - ```c++
    #include <iostream>
    using namespace std;
    
    class MyClass {
    public:
        MyClass() {
            cout << "Constructor called!" << endl;
        }
    
        MyClass(const MyClass& other) {
            cout << "Copy constructor called!" << endl;
        }
    
        ~MyClass() {
            cout << "Destructor called!" << endl;
        }
    };
    
    MyClass createObject() {
        MyClass obj;
        return obj; // 返回一个临时对象，调用拷贝构造函数
    }
    
    int main() {
        MyClass newObj = createObject(); // 调用createObject返回临时对象，触发拷贝构造函数
        return 0;
    }
    ```

  - ```c++
    Constructor called!
    Copy constructor called!
    Destructor called!
    Copy constructor called!
    Destructor called!
    Destructor called!
    ```

    值得注意的是C++会使用RPO优化，避免不必要的拷贝构造函数，这是禁用编译器的RVO优化后的结果。

### 20. 深拷贝与浅拷贝、移动构造函数

浅拷贝手写：

```cpp
#include <cstdio>
#include <string>
#include <iostream>
using namespace std;

class Vector{
private:

public:
    char* _array;
    Vector(string s){
        cout<<"调用构造函数"<<endl;
        int len = s.size();
        _array = new char[len+1];
        for (int i=0;i<len;i++)*(_array+i) = s[i];
        *(_array+len) = '\0';
    }
    // 浅拷贝
    Vector(Vector& v){
        cout<<"调用浅拷贝"<<endl;
        this->_array = v._array;
    }

    ~Vector(){
        cout<<"调用析构函数"<<endl;
        if (_array != nullptr){
            delete _array;
            _array = nullptr;//防止变成野指针
        }
    }
};
int main(){
    string s = "love mei";
    Vector* a = new Vector(s);
    Vector* b = new Vector(*a);
    cout<< b->_array <<endl;
    delete a;
    cout<< b->_array <<endl;
    delete b;
    return 0;
}
```

第二次输出b->_array时，会出现乱码，因为指向的内存已经被释放了。

这是因为b->_array和a->_array指向了同一片内存区域，当delete a的时候，该内存区域已经被收回，所以再用b->_array 访问那块内存实际上是不合适的，因为当delete b的时候，那块内存区域又被释放了一次，两次释放同一块内存，相当危险呀。

深拷贝手写：
 我们知道深拷贝，应该再调用拷贝构造函数时，应该为指针类型的成员单独动态分配一块内存，而不是直接赋值，两个指针指向同一块内存。

```cpp
#include <cstdio>
#include <string>
#include <iostream>
#include <cstring>
using namespace std;

class Vector{
private:

public:
    char* _array;
    Vector(string s){
        cout<<"调用构造函数"<<endl;
        int len = s.size();
        _array = new char[len+1];
        for (int i=0;i<len;i++)*(_array+i) = s[i];
        *(_array+len) = '\0';
    }
    // 深拷贝
    Vector(Vector& v){
        cout<<"调用深拷贝"<<endl;
        _array = new char[strlen(v._array)+1];
        strcpy(_array,v._array);
    }

    ~Vector(){
        cout<<"调用析构函数"<<endl;
        if (_array != nullptr){
            delete[] _array;
            _array = nullptr;//防止变成野指针
        }
    }
};
int main(){
    string s = "love mei";
    Vector* a = new Vector(s);
    Vector* b = new Vector(*a);
    cout<< b->_array <<endl;
    delete a;
    cout<< b->_array <<endl;
    delete b;
    return 0;
}
```

移动拷贝函数： 

移动拷贝构造函数是C++11引入的特性，是为了解决大数据情况下临时变量拷贝构造函数的开销过大问题。它将一个对象的资源（比如堆内存、文件句柄等）转移给另一个对象。

移动构造函数通常使用右值引用来实现，因为拷贝构造函数多是出现在初始化表达式、函数返回值这些临时变量，因此使用右值引用（&&）来实现

``` C++
#include <iostream>
#include <cstring>

class MyString {
private:
    char* data;

public:
    // 构造函数
    MyString(const char* str) {
        data = new char[strlen(str) + 1];
        strcpy(data, str);
        std::cout << "Constructor called!" << std::endl;
    }

    // 移动构造函数，会将原对象进行处理
    MyString(MyString&& other) noexcept : data(other.data) {
        other.data = nullptr; // 将原对象的资源指针置空，防止资源被释放两次
        std::cout << "Move Constructor called!" << std::endl;
    }

    // 析构函数
    ~MyString() {
        if (data != nullptr) {
            delete[] data;
        }
        std::cout << "Destructor called!" << std::endl;
    }

    // 输出字符串内容
    void print() {
        std::cout << "String: " << data << std::endl;
    }
};

// 函数返回一个临时对象，调用移动构造函数
MyString createString(const char* str) {
    return MyString(str);
}

int main() {
    // 创建临时对象并调用移动构造函数
    MyString str = createString("Hello, Move Constructor!");

    // 输出字符串内容
    str.print();

    return 0;
}

```

```c++ 
// 函数返回一个临时对象，而临时变量又是右值，因此调用参数为右值引用的移动构造函数（）
MyString createString(const char* str) {
    return MyString(str);
}
// createString("Hello, Move Constructor!")也是临时变量，因此进行类初始化时再次使用移动构造函数。
MyString str = createString("Hello, Move Constructor!");
```

### 20.为什么要使用移动语义/移动构造函数？

```c++
#include <iostream>
using namespace std;

class MyClass {
public:
    MyClass() {
        cout << "Constructor called!" << endl;
    }

    MyClass(const MyClass& other) {
        cout << "Copy constructor called!" << endl;
    }

    ~MyClass() {
        cout << "Destructor called!" << endl;
    }
};

MyClass createObject() {
    MyClass obj;
    return obj; // 返回一个临时对象，调用拷贝构造函数
}

int main() {
    MyClass newObj = createObject(); // 调用createObject返回临时对象，触发拷贝构造函数
    return 0;
}
```

以上的代码拷贝构造函数被调用两次，一次是生成临时值作为返回，另外一个便是newobj初始化时使用拷贝构造函数，若成员属性中有引用/指针并且指向非常大的内存时，频繁调用拷贝构造函数的代价是巨大的，并且临时对象在构造和释放一来一回也并无异议，因此使用移动构造函数来减少拷贝构造函数的开销。

### 20. 左值、右值

左值：是表达式结束后依然存在的持久对象（代表一个在内存中有确定对象），左值有变量名、可以取地址

右值：是表达式结束后不再存在的临时对象（不在内存中占有确定位置的对象）

### 21. 左值（lvalue）、将亡值（xvalue）、纯右值（rvalue）

C++11中使用两个独立的性质来区分类别：

- 是否拥有身份：指的是在内存中是否有明确的位置
- 是否可被移动：指的是可以放弃资源的所有权

按照这个两个性质可以分为三种基本类型：左值（lvalue）将亡值（xvalue）和纯右值（pvalue）。

- 拥有身份并且不可被移动的表达式称为左值：持久存在的对象/左值引用类型的返回值
- 拥有身份可以被移动的表达式称为将亡值：一般是为类型为右值引用的返回值
- 不拥有身份可以被移动的表示式称为纯右值：字面常量（“love mei”、5）、临时变量等
- 不拥有身份且不可被移动的表达式无法使用

```C++
Vector& func1();
Vector&& func2();
Vector func3();

int main(){
    Vector a;

    a;              //左值表达式
    func1();        //左值表达式，返还值是临时的，返还类型是左值引用，因此被认为不可移动。
    func2();        //将亡值表达式，返还值是临时的，返还类型是右值引用，因此指代的对象即使非临时也会被认为可移动。
    func3();        //纯右值表达式，返还值为临时值。
    std::move(a)；  //将亡值表达式，std::move本质也是个函数，同上。
    Vector();       //纯右值表达式
}
```

```c++
void func1(Vector v) {return;}
void func2(Vector & v) {return;}
void func3(Vector && v) {return;}
这三个函数的区别在于参数的类型和语义：

func1(Vector v): 这是传值方式。函数的参数会调用一次复制构造函数，产生参数的一个副本。在函数内部修改参数不会影响到原始对象，因为你在函数内部操作的是参数的副本。

func2(Vector & v): 这是传引用方式。函数的参数是一个左值引用，即传递的是原始对象的引用。在函数内部对参数的修改会直接影响到原始对象，因为你在函数内部操作的是原始对象本身。

func3(Vector && v): 这是传右值引用方式。函数的参数是一个右值引用，即传递的是一个临时对象（右值）。
```

### 20. 强转右值std::move

std::move并不能移动任何东西，他唯一的功能是将左值转化为右值，继而我们可以用右值引用引用这个值，以用于移动语义。

\23. 什么是内存泄漏

未释放、多次释放

### 24. C++11有什么新特性

- lambda表达式
- 右值引用和move语义
- 智能指针
- nullptr替换掉了null
- 类和结构体的初始化列表

## 操作系统



## 编程

### 接雨水

动态规划

```c++
class Solution {
public:

    int trap(vector<int>& height) {
        int sum = 0;
        int size = height.size();
        int max_left[size];
        int max_right[size];
        for (int i=0;i<size;i++){
             sum = max(sum,height[i]);
             max_left[i] = sum;
        }
        sum = 0;

        for (int i=size-1;i>=0;i--){
            sum = max(sum,height[i]);
            max_right[i] = sum;
        }
        sum = 0;
        for (int i=1;i<size-1;i++){
            if (min(max_left[i-1],max_right[i+1]) > height[i]){
                sum += min(max_left[i-1],max_right[i+1]) - height[i];
            }
        }
        return sum;
    }
};
```

单调栈

```c++
class Solution {
public:

    int trap(vector<int>& height) {
        int sum = 0;
        stack<int> st;
        st.push(0);
        for (int i=1;i<height.size();i++){
            if (height[i] <= height[st.top()] )st.push(i);
            else if (height[i] > height[st.top()] ){
                while (!st.empty() && (height[i] > height[st.top()]) ){
                    int top = st.top();
                    st.pop();
                    if (st.empty())break;
                    sum += (min(height[st.top()],height[i])-height[top])*(i-st.top()-1);
                }
                st.push(i);
            }
        }
        return sum;
    }
    
}
```

### 岛屿数量

BFS与DFS均可以

```c++
class Solution {
    int dx[4] = {-1,1,0,0};
    int dy[4] = {0,0,-1,1};
    int isvisited[310][310];
    int m,n;
public:
    int isinarea(int x,int y){
        if (x<0 || x>=m || y<0 || y>=n)return 0;
        else return 1;
    }
    void DFS(int x,int y,vector<vector<char>>& grid){
        isvisited[x][y] = 1;

        for (int i=0;i<4;i++){
            int tmp_x = x+dx[i];
            int tmp_y = y+dy[i];
            if ( isinarea(tmp_x,tmp_y) && isvisited[tmp_x][tmp_y] == 0 && grid[tmp_x][tmp_y]=='1'){
                DFS(tmp_x,tmp_y,grid);
            }
        }
    }
    void BFS(int x,int y,vector<vector<char> >& grid){
        queue<pair<int,int>> q;
        q.push(make_pair(x,y));
        isvisited[x][y] = 1;
        while (!q.empty()){
            pair<int,int> tmp = q.front();
            q.pop();
            for (int i=0;i<4;i++){
                for (int j=0;j<4;j++){
                        int tmp_x = tmp.first + dx[i];
                        int tmp_y = tmp.second + dy[i];
                    if ( isinarea(tmp_x,tmp_y) && isvisited[tmp_x][tmp_y] == 0 && grid[tmp_x][tmp_y]=='1'){
                        BFS(tmp_x,tmp_y,grid);
                    }
                }
            }
        }
    }
    int numIslands(vector<vector<char>>& grid) {
        int count =0 ;
        m = grid.size();
        n = grid[0].size();
        fill(&isvisited[0][0],&isvisited[0][0]+m*n,0);
        for (int i=0;i<m;i++){
            for (int j=0;j<n;j++){
                if (isvisited[i][j] == 0 && grid[i][j] == '1'){
                    BFS(i,j,grid);
                    count++;
                }
            }
        }
        return count;
    }
};
```

### 寻找峰值

二分查找：

```c++
class Solution {
public:
    int findPeakElement(vector<int>& nums) {
        int r = nums.size()-1;
        int l = 0;
        int mid;
        while (l < r){
            mid = l + (r-l)/2;
            if (nums[mid] >= nums[mid+1])r=mid;
            else if (nums[mid] < nums[mid+1])l=mid+1;
        }
        return l;
    }
};
```

### 设计链表

```c++
struct linkNode{
    int val;
    linkNode* next;
    linkNode():val(0),next(nullptr){}
    linkNode(int _val):val(_val),next(nullptr){}
    linkNode(int _val,linkNode* _next):val(_val),next(_next){}
};

class MyLinkedList {
private:
    linkNode* _dummynode;
    int _size;
public:
    MyLinkedList() {
        _dummynode = new linkNode();
        _size = 0;
    }

    int get(int index) {
        if (index >=_size)return -1;
        linkNode* cur = _dummynode;
        while (index--){
            cur = cur->next;
        }
        cur = cur->next;
        return cur->val;
    }

    void addAtHead(int val) {
        linkNode* newnode = new linkNode(val);
        newnode->next = _dummynode->next;
        _dummynode->next = newnode;
        _size++;
    }

    void addAtTail(int val) {
        linkNode* cur = _dummynode;
        while (cur->next!=nullptr){
            cur = cur->next;
        }
        linkNode* newnode = new linkNode(val);
        cur->next = newnode;
        _size++;
    }

    void addAtIndex(int index, int val) {
        linkNode* cur = _dummynode;
        if (index > _size)return ;
        while (index--){
            cur = cur->next;
        }
        linkNode* newnode = new linkNode(val);
        newnode->next = cur->next;
        cur->next = newnode;
        _size++;

    }

    void deleteAtIndex(int index) {
        linkNode* cur = _dummynode;
        if (index >= _size)return ;
        while (index--){
            cur = cur->next;
        }
        linkNode * deletenode = cur->next;
        cur->next = cur->next->next;
        delete deletenode;
        _size--;
    }
    void print(){
        linkNode* cur = _dummynode->next;
        while (cur!=nullptr){

            cout <<cur->val<<endl;
            cur = cur->next;
        }
    }

};
```

### 反转链表

```c++
struct linkNode{
    int val;
    linkNode* next;
    linkNode():val(0),next(nullptr){}
    linkNode(int _val):val(_val),next(nullptr){}
    linkNode(int _val,linkNode* _next):val(_val),next(_next){}
};

class MyLinkedList {
private:
    linkNode* _dummynode;
    int _size;
public:
    MyLinkedList() {
        _dummynode = new linkNode();
        _size = 0;
    }

    int get(int index) {
        if (index >=_size)return -1;
        linkNode* cur = _dummynode;
        while (index--){
            cur = cur->next;
        }
        cur = cur->next;
        return cur->val;
    }

    void addAtHead(int val) {
        linkNode* newnode = new linkNode(val);
        newnode->next = _dummynode->next;
        _dummynode->next = newnode;
        _size++;
    }

    void addAtTail(int val) {
        linkNode* cur = _dummynode;
        while (cur->next!=nullptr){
            cur = cur->next;
        }
        linkNode* newnode = new linkNode(val);
        cur->next = newnode;
        _size++;
    }

    void addAtIndex(int index, int val) {
        linkNode* cur = _dummynode;
        if (index > _size)return ;
        while (index--){
            cur = cur->next;
        }
        linkNode* newnode = new linkNode(val);
        newnode->next = cur->next;
        cur->next = newnode;
        _size++;

    }

    void deleteAtIndex(int index) {
        linkNode* cur = _dummynode;
        if (index >= _size)return ;
        while (index--){
            cur = cur->next;
        }
        linkNode * deletenode = cur->next;
        cur->next = cur->next->next;
        delete deletenode;
        _size--;
    }
    void print(){
        linkNode* cur = _dummynode->next;
        while (cur!=nullptr){

            cout <<cur->val<<endl;
            cur = cur->next;
        }
    }

};
```

### **调整数组顺序使奇数位于偶数前面**

```c++
class Solution {
public:
    void reOrderArray(vector<int> &array) {
        int temp;
        int _size = array.size();
        int i = 0;
        while (i<_size){
            if (array[i]%2==0){
                temp = array[i];
                array.erase(array.begin()+i);
                array.push_back(temp);
                _size--;
            }else i++;
        }

    }
};
```

### 判断是否有环并且找到环的入口结点

LCR 022

![i.png](https://pic.leetcode-cn.com/1633500700-vKehCR-i.png)

![j.png](https://pic.leetcode-cn.com/1633500864-oBbMil-j.png)

```C++
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode(int x) : val(x), next(NULL) {}
 * };
 */
class Solution {
public:
    ListNode *detectCycle(ListNode *head) {
        // 空链表 一个节点 两个节点
        if (head == nullptr || head->next==nullptr || head->next->next == nullptr)return nullptr;
        ListNode* slow = head->next;
        ListNode* fast = head->next->next;

        while (fast!=slow){
            if (fast->next == nullptr || fast->next->next == nullptr)return nullptr;
            fast = fast->next->next;
            slow = slow->next;
        }
        // 快节点设置到开头，两者以速度为1第二次相遇即是入口节点
        fast = head;
        while (fast != slow){
            fast = fast->next;
            slow = slow->next;
        }
        return fast;
    }
};
```

### 相交链表

若相交，链表A： a+c, 链表B : b+c. a+c+b+c = b+c+a+c 。则会在公共处c起点相遇。若不相交，a +b = b+a 。因此相遇处是nullptr

```c++
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode(int x) : val(x), next(NULL) {}
 * };
 */
class Solution {
public:
    ListNode *getIntersectionNode(ListNode *headA, ListNode *headB) {
        if (headA == nullptr || headB == nullptr)return nullptr;
        ListNode* A = headA;
        ListNode* B = headB;
        while (A != B){
            A = (A == nullptr) ? headB:A->next;
            B = (B == nullptr) ? headA:B->next;
        }
        return (A==nullptr)? nullptr:A;
        
    }
};
```

### 删除链表的倒数第K个节点

使用双指针p和q，让p和q相差k时再同时移动，当p->next==nullptr时，q->next就是倒数第k个节点。

```c++
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode() : val(0), next(nullptr) {}
 *     ListNode(int x) : val(x), next(nullptr) {}
 *     ListNode(int x, ListNode *next) : val(x), next(next) {}
 * };
 */
class Solution {
public:
    ListNode* removeNthFromEnd(ListNode* head, int n) {
        ListNode* _dummynode = new ListNode(0,head);
        ListNode* fast = _dummynode;
        ListNode* slow = _dummynode;
        int i = 0;
        while (fast->next != nullptr){
            if (i<n){
                fast = fast->next;
                i++;
                continue;
            }
            fast=fast->next;
            slow=slow->next;
        }
        slow->next = slow->next->next;
        
        return _dummynode->next;
    }
};
```

### 层序顺序构造二叉树

```c++
#include <iostream>
#include <vector>
#include <queue>

using namespace std;

struct Treenode {
    int val;
    Treenode* left;
    Treenode* right;
    Treenode(int _val) : val(_val), left(nullptr), right(nullptr) {}
};

Treenode* constructBinaryTree(vector<int> levelorder) {
    if (levelorder.size() == 0 || levelorder[0] == -1) return nullptr;

    Treenode* root = new Treenode(levelorder[0]);
    queue<Treenode*> q;
    q.push(root);
    int i = 1;

    while (i < levelorder.size()) {
        Treenode* current = q.front();
        q.pop();

        if (levelorder[i] != -1) {
            Treenode* newnode = new Treenode(levelorder[i]);
            current->left = newnode;
            q.push(newnode);
        }
        i++;

        if (levelorder[i] != -1 && i < levelorder.size()) {
            Treenode* newnode = new Treenode(levelorder[i]);
            current->right = newnode;
            q.push(newnode);
        }
        i++;
    }
    return root;
}

void inorder(Treenode* root) {
    if (root == nullptr) return;

    inorder(root->left);
    cout << root->val << endl;
    inorder(root->right);
}

int main() {
    vector<int> levelorder = {1, 2, 3, -1, 4, 5};
    Treenode* root = constructBinaryTree(levelorder);

    cout << "中序遍历结果: " << endl;
    inorder(root);

    return 0;
}

```

### 二叉树的前序、中序、后序和层序遍历

前序、中序、后序指的是子树按照什么顺序访问根结点

前序：

```c++
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode() : val(0), left(nullptr), right(nullptr) {}
 *     TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
 *     TreeNode(int x, TreeNode *left, TreeNode *right) : val(x), left(left), right(right) {}
 * };
 */
class Solution {
public:
    vector<int> v;
    void preorder(TreeNode* root){
        if (root == nullptr)return;
        v.push_back(root->val);
        preorder(root->left);
        preorder(root->right);
    }
    vector<int> preorderTraversal(TreeNode* root) {
        preorder(root);
        return v;
    }
};
```

中序：

```c++
class Solution {
public:
    vector<int> v;
    void inorder(TreeNode* root){
        if (root == nullptr)return;
        inorder(root->left);
        v.push_back(root->val);
        inorder(root->right);
    }
    vector<int> inorderTraversal(TreeNode* root) {
        inorder(root);
        return v;
    }
};
```

后续：

```c++
class Solution {
public:
    vector<int> v;
    void postorder(TreeNode* root){
        if (root == nullptr)return;
        postorder(root->left);
        postorder(root->right);
        v.push_back(root->val);
    }
    vector<int> postorderTraversal(TreeNode* root) {
        postorder(root);
        return v;
    }
};
```

层序遍历：

```c++
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode() : val(0), left(nullptr), right(nullptr) {}
 *     TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
 *     TreeNode(int x, TreeNode *left, TreeNode *right) : val(x), left(left), right(right) {}
 * };
 */
class Solution {
public:
    vector<vector<int> > res;
    void levelorder(TreeNode* root){
        if (root==nullptr)return ;
        vector<int> temp;
        queue<TreeNode*> q;
        q.push(root);
        temp.push_back(root->val);
        res.push_back(temp);
        temp.clear();
        while (!q.empty()){
            int cnt = q.size();
            TreeNode* current;
            
            while (cnt--){
                current = q.front();
                q.pop();
                if (current->left != nullptr){

                    q.push(current->left);
                    temp.push_back(current->left->val);
                }
                if (current->right != nullptr){
                    q.push(current->right);
                    temp.push_back(current->right->val);
                }
            }
            if (temp.size()){
                res.push_back(temp);
                temp.clear();
            }


        }
    }
    vector<vector<int>> levelOrder(TreeNode* root) {
        levelorder(root);
        return res;
    }
};
```

### 二叉树的最大深度

深度和高度是计算顺序是相反的，因而使用的遍历顺序也不同

高度 是从下往上 使用后序遍历（左子树、右子树、根结点）的方式，可以先求得两颗子树的高度，然后根据两子树的高度计算出根结点当前的高度。

而深度 是从上往下的 使用前序遍历（根结点、左子树、右子树）的方式，先遍历的是根结点，再是左右子树，因而前序遍历求深度时，需要自己携带自己的深度，以便于传给左右子树。

后续遍历：

```c++
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode() : val(0), left(nullptr), right(nullptr) {}
 *     TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
 *     TreeNode(int x, TreeNode *left, TreeNode *right) : val(x), left(left), right(right) {}
 * };
 */
class Solution {
public:
    int maxDepth(TreeNode* root) {
        if (root == nullptr)return 0;
        int leftheight = maxDepth(root->left);
        int rightheight = maxDepth(root->right);

        return 1 + max(leftheight,rightheight);
    }
};
```

前序遍历：（值从上往下遍历，因此函数需要携带参数）

```c++
class Solution {
public:
    int result = 0;
    void maxdepth(TreeNode* root,int depth){
        result = depth > result ? depth : result; // 更新最大深度
    if (root==nullptr) return ;
    if (root->left != nullptr){
        maxdepth(root->left,depth+1);
    } 
    if (root->right != nullptr){
        maxdepth(root->right,depth+1);
    }
    return ;

    }
    int maxDepth(TreeNode* root) {
        if (root != nullptr)maxdepth(root,1);
        return result;
    }
};
```

### 二叉树的最小深度

主要在于更新值的条件和结束的条件都在叶子节点的时候

而最大深度是每个节点都要计算，而结束的条件在于其为空

前序遍历：

```c++
class Solution {
public:
    int result;
    void mindepth(TreeNode* root,int depth){
        if (root->left==nullptr && root->right == nullptr){
            // 判断是否为叶子节点。
            result = depth < result ? depth:result;
            return;
        }
        if (root->left != nullptr){
            mindepth(root->left,depth+1);
        }
        if (root->right != nullptr){
            mindepth(root->right,depth+1);
        }
    }
    int minDepth(TreeNode* root) {
        if (root!=nullptr){
            result = INT_MAX;
            mindepth(root,1);
        }else result = 0;
        
        return result;
    }
};
```

后序遍历：

```c++
class Solution {
public:
    int mindepth(TreeNode* root){
        if (root->left==nullptr && root->right == nullptr){
            return 1;
        }
        int left_height = INT_MAX,right_height = INT_MAX;
        if (root->left != nullptr)left_height = mindepth(root->left);
        if (root->right != nullptr)right_height = mindepth(root->right);
        return 1+min(left_height,right_height);
    }
    int minDepth(TreeNode* root) {
        if (root==nullptr)return 0;
        else return mindepth(root);
    }
};
```

### 二叉树的右视图

我们按照 「根结点 -> 右子树 -> 左子树」 的顺序访问，就可以保证每层都是最先访问最右边的节点的。再使用depth与结果vector的大小确认是否为第一次访问。（因为有一部分右视图出现在左子树，左子树的深度比右子树的深度高）

```c++
class Solution {
public:
    int result = 0;
    void maxdepth(TreeNode* root,int depth){
        result = depth > result ? depth : result; // 更新最大深度
    if (root==nullptr) return ;
    if (root->left != nullptr){
        maxdepth(root->left,depth+1);
    } 
    if (root->right != nullptr){
        maxdepth(root->right,depth+1);
    }
    return ;

    }
    int maxDepth(TreeNode* root) {
        if (root != nullptr)maxdepth(root,1);
        return result;
    }
};
```

### 翻转二叉树

```c++
class Solution {
public:
    void DFS(TreeNode* root){
        if (root == nullptr)return ;
        swap(root->left,root->right);
        DFS(root->left);
        DFS(root->right);
    }
    TreeNode* invertTree(TreeNode* root) {
        DFS(root);
        return root;
    }
};
```

### 对称二叉树

```c++
class Solution {
public:
    bool compare(TreeNode* left,TreeNode* right){
        // 列举直接可以返回的情况 以及返回的边界条件
        if (left == nullptr && right == nullptr)return true;
        else if (left == nullptr && right != nullptr)return false;
        else if (left != nullptr && right == nullptr)return false;
        else if (left->val != right->val)return false;

        bool a = compare(left->left,right->right);
        bool b = compare(left->right,right->left);

        return a && b;
    }
    bool isSymmetric(TreeNode* root) {
        return compare(root->left,root->right);
    }
};
```

### 创建二叉搜索树BST

```c++
#include <iostream>
#include <vector>
#include <queue>

using namespace std;

struct Treenode {
    int val;
    Treenode* left;
    Treenode* right;
    Treenode(int _val) : val(_val), left(nullptr), right(nullptr) {}
};

Treenode* insert(Treenode* root,int x){
    // 节点为空，直接创建一个新的节点
    if (root == nullptr){

        root = new Treenode(x);
    }
    if (x < root->val){
        // 新节点应该插入到当前节点的左子树中
        root->left = insert(root->left,x);
    }else if (x > root->val){
        // 新节点应该插入到当前节点的右子树中
        root->right = insert(root->right,x);
    }

    return root;

}
Treenode* Construct_BST(Treenode* root,vector<int> values){
    for (int i=0;i<values.size();i++){
        root = insert(root,values[i]);
    }
    return root;
}


void inorder(Treenode* root) {
    if (root == nullptr) return;

    inorder(root->left);
    cout << root->val << " ";
    inorder(root->right);
}

int main() {
    vector<int> values = {1, 2, 3, -1, 4, 5};

    Treenode* root = nullptr;
    root = Construct_BST(root,values);

    cout << "中序遍历结果: " << endl;
    inorder(root);

    return 0;
}
```

### 快排

```c++
void quicksort(vector<int>& arr,int low,int high){
    if (low < high){
        int pivot = arr[low];
        int left = low+1;
        int right = high;
        while (left <= right){
            if (arr[left] >pivot && arr[right]<pivot){
                swap(arr[left],arr[right]);
            }
            while (arr[left]<=pivot && left <= right){
                left++;
            }
            while (arr[right]>=pivot && left <= right){
                right--;
            }

        }
        swap(arr[low],arr[right]);
        quicksort(arr,low,right-1);
        quicksort(arr,right+1,high);
    }
}
```







