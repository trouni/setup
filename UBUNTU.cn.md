# 电脑设置教程

以下的教程将会帮助你为接下来在[Le Wagon](http://www.lewagon.org) 全栈开发训练营中做好准备：

- 获取一个文本编辑器，这里将会是你日日夜夜花时间的地方
- 安装一个软件包管理器
- 装扮你的终端
- 配置git和GitHub
- 安装Ruby


## 远程工具

为了能让我们不在一起的时候也能很好的沟通，我们将会使用以下两个工具：

### Zoom

⚠️ 如果你已经安装了Zoom，请确保你Zoom的版本不低于**5.4**。否则，你将不能使用分组讨论室来和你的伙伴一起工作。

Zoom是一个视频会议工具。想要创建账户并安装这个应用，你需要到[https://zoom.us/download](https://zoom.us/download)这个网页，并在**Zoom会议客户端（Zoom Client for Meetings）**下方点击**下载（Download）**按钮。打开你刚下载好的文件。将出现一个进度条，然后Zoom便会开始。点击**Connection** 并创建一个账户，选择**Sign Up Free**选项：

![zoom-sign-up-free.png](images/zoom-sign-up-free.png)

当你连接成功后，你将会看到:

![zoom-welcome-screen.png](images/zoom-welcome-screen.png)

现在你可以关闭Zoom了。


## GitHub账户

你有注册好GitHub账户嘛？如果还没有，[现在注册](https://github.com/join)。

:point_right: **[上传一张照片](https://github.com/settings/profile)** 并在你的GitHub账户中设置你的名称。这一步很重要，因为我们将使用一个带有你头像的内部dashboard。请**现在**立即做这一步，然后再去继续下面的步骤。

![](images/github_upload_picture.png)


## Git

To install `git`, first open a terminal. To open a terminal, you can click on the Ubuntu Start button in the sidebar and type `Terminal`. Then click on the terminal icon.

Then copy this line with `Ctrl` + `C`:

```bash
sudo apt install -y git
```

:bulb: To **paste it in the terminal**, you need to use `Ctrl` + `Shift` + `V`.


Let's now install GitHub [official CLI](https://cli.github.com) (Command Line Interface) with the following commands:

```bash
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-key C99B11DEB97541F0
sudo apt-add-repository https://cli.github.com/packages
sudo apt update
sudo apt install -y gh
```

To check that `gh` has been successfully installed on your machine, you can run:

```bash
gh --version
```

If you don't get a prompt saying `gh version X.Y.Z (YYYY-MM-DD)` with at least version 1.4, please refer to [the documentation](https://github.com/cli/cli/blob/trunk/docs/install_linux.md#official-sources) where they list some troubleshooting information. In doubt, ask a TA.


## Sublime Text 3 - Your text editor

A text editor is one of the most important tools of a developer.
Follow these instructions in the Terminal:

```bash
wget -qO - https://download.sublimetext.com/sublimehq-pub.gpg | sudo apt-key add -
```

:point_up: This command will ask for your password with: `[sudo] password for <username>:`. Don't panick! Calmy type your password key by key. You won't have a visual feedback (like little `*`), that's **perfectly normal**, keep on typing. When you're done, hit `Enter` :muscle:.

```bash
sudo apt install -y apt-transport-https
echo "deb https://download.sublimetext.com/ apt/stable/" | sudo tee /etc/apt/sources.list.d/sublime-text.list
sudo apt update
sudo apt install -y sublime-text
```

Sublime Text is free without any time limitation but a popup will appear every ten saves to remind you there is a license to buy. You can hit `Esc` when this happens, but feel free to buy Sublime Text if you really like this one (there are alternatives).


## Oh-my-zsh - Fancy your Terminal

We will use the shell named `zsh` instead of `bash`, the default one.

```bash
sudo apt install -y zsh curl vim imagemagick jq
sh -c "$(curl -fsSL https://raw.githubusercontent.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"
# it will ask for your session password
```

Be careful, those commands will ask you to type your password twice. At the end
your prompt should look like this:

![](images/ubuntu_oh_my_zsh.png)

If it doesn't, **ask a teacher**.

To make this change stick, restart your laptop (or virtual machine):

```bash
sudo reboot
```


## GitHub

我们需要生成SSH密钥。这些会在GitHub和Heroku上使用。把它当成一种登陆的方式好了，但它和平时用的用户名和密码不一样。如果你之前有生成过密钥，你就可以跳过这个步骤。

打开终端，然后输入下面的命令，把email换成**你自己的**（应该用你注册GitHub的email）。然后它会提示你一些信息。按回车键，直到它问你要**密码**。

```bash
mkdir -p ~/.ssh && ssh-keygen -t ed25519 -o -a 100 -f ~/.ssh/id_ed25519 -C "TYPE_YOUR_EMAIL@HERE.com"
```

**敲黑板：** 当它问你要密码时，输入你想要的密码（并且是你可以记住的密码）。这个密码会保护你保存在硬盘上的私钥。你输入的时候，还是不会在屏幕上看到任何东西，这是**正常的！**输入密码，当你输完的时候，按下回车。

然后你需要把**公钥**存到GitHub上。运行下面的命令：

```bash
cat ~/.ssh/id_ed25519.pub
```

它会在屏幕上显示`id_ed25519.pub`文件的内容。


- 复制出现在`ssh`的内容（公钥）粘贴到你邮箱地址的末尾
- 打开[github.com/settings/ssh](https://github.com/settings/ssh)
- 点击绿色的按钮`New SSH key`
- 填你的电脑的名称 （可以自己取一个，比如`My Windows`）
- 粘贴**公钥**
- 点击绿色按钮**Add key**，就完成这个步骤了


再检查一下，在终端里运行：

```bash
ssh -T git@github.com
```

:warning: 它会显示一个警告提示，输入`yes`，然后敲击`Enter`。

这个是应该看到的结果:

```
# Hi --------! You've successfully authenticated, but GitHub does not provide shell access
```

&nbsp;

&nbsp;&nbsp;&nbsp; :white_check_mark: 如果你看到这条信息，那说明密钥已经被成功加上了！

&nbsp;&nbsp;&nbsp; :x: 如果你看到错误提示，你需要重新试试。别忘了你可以*叫老师来帮忙*。


---

#### :wrench: 故障排查

<details>
  <summary>如果<code>ssh -T git@github.com</code> 不行的话</summary>

  &nbsp;


  运行下面的命令，然后再尝试一遍:

  ```bash
  ssh-add ~/.ssh/id_ed25519
  ```
  </details>

---


别着急，花点时间看看[这篇文章](http://sebastien.saunier.me/blog/2015/05/10/github-public-key-authentication.html)来更好地了解那些密钥都是干什么用的。


## GitHub CLI

CLI是[Command-line Interface（命令行界面）](https://baike.baidu.com/item/%E5%91%BD%E4%BB%A4%E8%A1%8C%E7%95%8C%E9%9D%A2/9910197?fr=aladdin)的首字母缩写。

在这一章节里面，我们会安装[GitHub CLI](https://cli.github.com/)。这样我们就可以从终端链接GitHub的数据，执行一些有用的动作。

之前执行的命令应该已经安装了GitHub CLI。首先你需要**登陆**。复制下面的命令（**不要**更改它），然后复制到终端，敲击回车：

```bash
gh auth login -s 'user:email' -w
```

你会看到下面的输出结果：

```bash
- Logging into github.com
! First copy your one-time code: 0EF9-D015
- Press Enter to open github.com in your browser...
```

复制那段验证码（code）(在上面的例子中是`0EF9-D015` ），然后敲击`Enter`。你的浏览器就会打开一个页面让你授权GitHub CLI使用你的GitHub账号。同意，并等待一会儿。回到终端，再次敲击`回车`，然后就应该好啦:tada:

检查一下你有没有链接好：

```bash
gh auth status
```

如果你看到`Logged in to github.com as <你的GitHub用户名> `，那就可以了。如果没有，**问问老师**。

然后运行下面的配置命令:

```bash
gh config set git_protocol ssh
```

最后，新建一个[gist](https://docs.github.com/en/free-pro-team@latest/github/writing-on-github/editing-and-sharing-content-with-gists)来确保`gh` 可以正常运作：

```bash
echo "Hello [Le Wagon](https://www.lewagon.com) :wave:" | gh gist create -d "Starting my coding journey..." -f "SETUP_DAY.md" -p -w
```

这一行命令会在你的浏览器里打开刚创建的gist页面。看呐，我们刚创建了一个[**Markdown**](https://guides.github.com/features/mastering-markdown/)文件！


## Dotfiles (标准配置)

黑客很喜欢把他们的shell和工具变得很酷炫。

让我们用Le Wagon提供的一个超棒的默认配置文件来开始吧：[`lewagon/dotfiles`](http://github.com/lewagon/dotfiles).

因为你的配置是私人的，所以你需要保存在**自己**的代码库里（repository/repo）。Fork的意思是：在你的GitHub账号上建一个新的代码库，和原始的那一个是一模一样的（可以想象成你在复制粘贴这个代码库）。
这样，你在你的GitHub上就会有一个新的代码库： `$GITHUB_USERNAME/dotfiles`。
我们需要fork，因为每个人都需要在那些文件里加上一些**特定**信息（比如你的名字）。

打开终端，运行下面的命令：

```bash
export GITHUB_USERNAME=`gh api user | jq -r '.login'`
echo $GITHUB_USERNAME
```

你就能看到你的GitHub用户名在终端里显示出来了。
如果没有的话，现在就**停下**，找老师帮忙。看起来之前的步骤(`gh auth`)有一些问题。

现在就可以fork代码库（repo)，然后克隆到你自己的电脑上了：

```bash
mkdir -p ~/code/$GITHUB_USERNAME && cd $_
gh repo fork lewagon/dotfiles --clone
```

运行`dotfiles`安装器：

```bash
cd ~/code/$GITHUB_USERNAME/dotfiles && zsh install.sh
```

用下面的命令检查一下你GitHub账号录入的电子邮箱。你需要在其中选一个（如果你有好几个的话），然后再进入下一个步骤：

```bash
gh api user/emails | jq -r '.[].email'
```

运行git安装器：

```bash
cd ~/code/$GITHUB_USERNAME/dotfiles && zsh git_setup.sh
```

:point_up: 这会**提示**填写你的全名（`FirstName LastName`）和你的邮箱。注意啦，你**需要**填`gh api ...`命令列出的其中一个电子邮箱。不然，Kitt就没办法跟进你的学习进程。

现在**退出**你刚打开的所有终端窗口。


### Sublime Text 自动配置

打开一个新的终端并输入：

```bash
cd ~/code
stt
```

它将会**在Sublime Text中打开当前文件夹**。这是我们如何使用它的方法。

**关闭Sublime Text**并重新打开它：

```bash
stt
```

**等待一分钟**，等所有额外的软件包都自动安装好（会自动打开一个带有文本的新的窗口，上面会包含每个你安装好的新包的文档）。如果想要跟踪软件包的安装进度，你可以前往`View > Show console`。

如果想要核查是否所有的插件都安装好了，你可以打开`命令面板 Command Palette`(在OSX上，按下`⌘` + `⇧` + `P`；在linux上，按下`Ctrl` + `⇧` + `P`)，输入`Packlist`然后按`Enter`，你应该会看到有一些软件包被安装了（像是[Emmet](http://emmet.io/)）。

当这些结束之后，你可以关闭Sublime Text。


