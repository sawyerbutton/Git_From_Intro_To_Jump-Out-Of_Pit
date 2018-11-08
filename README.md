# Git_From_Intro_To_Jump-Out-Of_Pit

## Git从入门到跳坑

### Git是什么

- Git是一个开源的分布式版本管理系统

> 将这一描述拆分成不同的部分来看

- 控制系统

> 控制系统代表着Git是一个内容跟踪器。这意味着Git可以用来存储内容，而根据Git提供的其他功能来看，Git最常见的用途是存储代码

- 版本控制系统

> 存储在Git中代码将随着代码内容的增加而增加，不同的开发者可以并行地增加Git中的代码，而版本控制系统帮助去处理维护修改和变更的记录

- 分布式版本管理系统

> Git拥有一个存储在服务器上的远程仓库和一个存储在每个开发者机器上的的本地仓库。 这意味着代码并不仅仅存储在中央服务器中，完全的代码拷贝也存在于所有开发者的电脑中。 这也是为什么Git被称为`分布式`版本管理系统的原因

### 为什么Git是需要的

- 现实生活中项目通常有多个开发者并行开发，而Git这样的分布式版本管理工具可以保证在开发者之间没有存在代码冲突

- 除此之外，现实生活中需求的变化也是很正常的状况，版本控制系统允许开发者返回/`回退`到旧版本的代码中去

- 而有时几个并行运行的项目涉及相同的代码库，在这种情况下，Git中的`branch`将会大放异彩

### 如何使用Git

#### 下载Git

- ![使用这个链接以获取多操作系统安装Git的教程](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git)

> 安装完成后使用下述命令验证Git是否安装成功

```bash
git --version
```

#### 创造第一个本地Git仓库

- 在本地创建一个文件夹，比如`simple-git-repo`

- 进入文件夹中并初始化一个本地Git仓库，比如

```bash
cd simple-git-demo 
git init
```

- `git init`指令将会初始化出一个本地仓库

- 在本地创建一个`demo.ts`文件， 并向其中添加内容如`const demo = '我是Demo'`

> 创建什么类型的文件在此时并不重要，`ts`文件也可以被替换为`js`，`html`,`java`文件

#### 准备(staging)和提交(commiting)代码

- `staging`原本的含义是舞台，这里我意指为准备就绪

- 提交是将代码添加到本地仓库的的过程

- 在提交代码之前，需要将被提交的代码放置在准备区，而准备区是跟踪了所有需要被提交的代码的地方

- 任何不处于准备区的代码都不会被提交到本地代码库中。换言之这给与了开发者选择性提交内容的能力

> 放置`demo.ts`文件到准备区

```bash
git add demo.ts
```

> 假设你不仅仅有`demo.ts`文件也有其他一些文件`file1`,`file2`,`file3`, 而希望将他们都放置进准备区

```bash
git add file1 file2 file3
```

> 假设你希望将文件夹中所有的文件都放置进准备区(需要注意的是，他会将`所有`的`文件和文件夹`都放入准备区)

```bash
git add .
```

#### Git状态和Git记录

- 修改`demo.ts`文件并增加一行内容`const demo2 = '我是Demo2'`

```typescript
const demo = '我是Demo';
const demo2 = '我是Demo2';
```

> 使用`git status`可以观察到什么文件发生了变化以及在准备区的文件以及一些其他信息(之后再说)

```bash
git status
```

> 控制台将会展示`demo.ts`文件已经被修改但是并没有在准备区就绪

```bash
modified:   demo.ts
```

> 使用下述指令将`demo.ts`文件添加至准备区并提交他们

```bash
git add demo.ts
git commit -m "demo.ts file has been modified"
```

- 使用`log`指令可以打印出所有迄今为止的提交

```bash
git log
```

> 事实上，`log`将会显示每个提交的作者，提交的日期和相应的提交消息

#### Git分支

- 默认情况下，`git commit`将会作用于`master`分支，但是什么是`master`分支？

> 分支是指向Git仓库中最新提交的指针

> 换言之，上述操作中的主分支为指向了第二次提交`demo.ts`文件修改的指针

> 分支在多开发者平行开发时是不可或缺的

![git分支](./assets/1.png)

- 初始化时，提交1和提交2在主分支上完成，在提交2完成后创建了一个新的自分支，提交3和提交4同时分别在主分支和自分支上分别完成

- 主分支和子分支在提交2之后分道扬镳，两者分别拥有不同的代码

- 子分支可以通过`merge`命令合并到主分支中

##### 创建一个本地Git分支

- 使用如下命令创造一个`test`分支

```bash
git branch test
```

- 上述指令只是创造了新的`test`分支，此时我们仍然处在主分支中，通过`checkout`指令可以切换到`test`分支中

```bash
git checkout test
```

- 当需要查看所有的本地分支时可以使用如下指令

```bash
git branch
```

##### 在test分支上修改一些内容

- 在test分支上的`demo.ts`文件中增加内容`const demo3 = '我是test分支的demo'`

- 就绪并提交上述修改

```bash
git add demo.ts
git commit -m "test branch commit"
```

- 上述的提交在`test`分支上完成，现在`test`分支拥有两次提交，比主分支多一次提交，

- 值得记住的是,可以使用`git log`指令查看你在当前分支上的提交记录

