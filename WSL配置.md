# WSL配置

安装WSL2配置

## Ubuntu

右键开始菜单，以管理员身份打开命令行或 Powershell，然后输入：

```bash
wsl --install
```

**安装完成后需要重启电脑**。默认会安装 Ubuntu，如果想安装其他 Linux 系统的话，可以先`wsl —list —online`列出可用的系统，然后`wsl —install -d <Distribution Name>`安装对应系统。

- 用户名和密码

装好之后，在开始菜单找到 Ubuntu 并打开，第一次是需要设置用户名和密码的，这个用户名密码也是具备管理员`sudo`权限的。



## zsh/oh-my-zsh

zsh 比 bash 更加强大也更好看，配合 oh-my-zsh 和相关插件，可以实现命令高亮、命令补全、git 快捷操作等等。

```bash
# 更新 package
sudo apt update && sudo apt upgrade

# 安装 zsh
sudo apt install zsh -y

# 安装 oh-my-zsh
wget https://github.com/robbyrussell/oh-my-zsh/raw/master/tools/install.sh -O - | zsh || true

# 安装命令补全和高亮插件
git clone https://github.com/zsh-users/zsh-syntax-highlighting.git ~/.oh-my-zsh/plugins/zsh-syntax-highlighting
git clone https://github.com/zsh-users/zsh-autosuggestions ~/.oh-my-zsh/plugins/zsh-autosuggestions
sed -i 's/plugins=(git)/plugins=(git zsh-autosuggestions zsh-syntax-highlighting)/g' ~/.zshrc

# 将 zsh 设置为默认的shell
chsh -s /bin/zsh
```



配置好之后下次打开默认就是 zsh 了，也可以输入`zsh`进入 zsh 环境。另外，我会在 zsh 的配置文件中设置一些常用的指令。编辑配置文件`vim .zshrc`，不习惯 vim 的话，可以用 VSCode 打开`code .zshrc`，在最后加入：

```bash
# 列表形式显示所有文件详情
alias ll="ls -alF"
# 删除文件前需确认
alias rm="rm -i"
```



## Git

Git 默认会忽略大小写，很多人都遇到过这个坑，所以最好配环境的时候配好：

```bash
# 启用大小写敏感
git config --global core.ignorecase false
```



剩下的就是常规配置了，比如用户名和邮箱、生成 public key 等等：

```bash
# 配置用户名和密码
git config --global user.name "Your Name"
git config --global user.email "youremail@domain.com"

# 生成 ssh key
# 用 Github 的话，可以拷贝生成的公钥到 https://github.com/settings/keys
ssh-keygen
```



## VSCode

在 VSCode 中安装[Remote Development](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.vscode-remote-extensionpack)插件就能在 VSCode 中直接将 WSL 作为开发环境，非常方便：

![img](https://cos.codec.wang/wsl2-frontend-vscode-remote.jpg)

另外如果目录是存储在 WSL 下面，那么在 Windows 下用 VSCode 打开这个目录的时候就会提示让你在 WSL 环境下打开：

![img](https://cos.codec.wang/wsl2-frontend-vscode-reopen-in-wsl.jpg)



## 文件系统

需要注意的是我们现在有了两套系统，两者的文件类型并不一致，跨系统访问和传输文件的话效率会下降很多，最好各存各的，以用户目录为例：

- 如果在 Windows 上开发，就将文件放在：`C:\Users\<UserName>\`
- 如果在 Ubuntu 上开发，就将文件放在：`\\wsl$\ubuntu\home\<UserName>\`

想在 WSL 里用资源管理器打开目录的话，可以输入`explorer.exe .`。另外，Windows 的文件路径在 Ubuntu 上会挂载到`/mnt/`，比如在 WSL 里访问 Windows C 盘的用户目录就是`cd /mnt/c/Users/<UserName>/`。



## Proxy

```shell
#!/bin/sh
hostip=$(cat /etc/resolv.conf | grep nameserver | awk '{ print $2 }')
wslip=$(hostname -I | awk '{print $1}')
port=7890
 
PROXY_HTTP="http://${hostip}:${port}"
 
set_proxy(){
  export http_proxy="${PROXY_HTTP}"
  export HTTP_PROXY="${PROXY_HTTP}"
 
  export https_proxy="${PROXY_HTTP}"
  export HTTPS_proxy="${PROXY_HTTP}"
 
  export ALL_PROXY="${PROXY_SOCKS5}"
  export all_proxy=${PROXY_SOCKS5}
 
  git config --global http.https://github.com.proxy ${PROXY_HTTP}
  git config --global https.https://github.com.proxy ${PROXY_HTTP}
 
  echo "Proxy has been opened."
}
 
unset_proxy(){
  unset http_proxy
  unset HTTP_PROXY
  unset https_proxy
  unset HTTPS_PROXY
  unset ALL_PROXY
  unset all_proxy
  git config --global --unset http.https://github.com.proxy
  git config --global --unset https.https://github.com.proxy
 
  echo "Proxy has been closed."
}
 
test_setting(){
  echo "Host IP:" ${hostip}
  echo "WSL IP:" ${wslip}
  echo "Try to connect to Google..."
  resp=$(curl -I -s --connect-timeout 5 -m 5 -w "%{http_code}" -o /dev/null www.google.com)
  if [ ${resp} = 200 ]; then
    echo "Proxy setup succeeded!"
  else
    echo "Proxy setup failed!"
  fi
}
 
if [ "$1" = "set" ]
then
  set_proxy
 
elif [ "$1" = "unset" ]
then
  unset_proxy
 
elif [ "$1" = "test" ]
then
  test_setting
else
  echo "Unsupported arguments."
fi

```



```shell
# 列表形式显示所有文件详情
alias ll="ls -alF"
# 删除文件前需确认
alias rm="rm -i"

alias proxy="source /home/ubuntu/proxy.sh"
```



## DeepLearning配置
