## 给新mac配环境

#### Homebrew

```bash
# https://brew.idayer.com/guide/start/
/bin/bash -c "$(curl -fsSL https://cdn.jsdelivr.net/gh/ineo6/homebrew-install/install.sh)"
```

#### c++

```bash
gcc
```

#### java

```bash
brew tap mdogan/zulu

brew install <name>

/usr/libexec/java_home -V

```

| **JDK**         | **Cask Name** |
| --------------- | ------------- |
| OpenJDK 7       | zulu-jdk7     |
| OpenJDK 8       | zulu-jdk8     |
| OpenJDK 9       | zulu-jdk9     |
| OpenJDK 10      | zulu-jdk10    |
| OpenJDK 11      | zulu-jdk11    |
| OpenJDK 12      | zulu-jdk12    |
| OpenJDK 13      | zulu-jdk13    |
| OpenJDK 14      | zulu-jdk14    |
| OpenJDK 15      | zulu-jdk15    |
| OpenJDK 16      | zulu-jdk16    |
| OpenJDK 17      | zulu-jdk17    |
| OpenJDK 18      | zulu-jdk18    |
| OpenJDK 19      | zulu-jdk19    |
| OpenJDK 20      | zulu-jdk20    |
| Mission Control | zulu-mc       |

#### python

```bash
brew install miniconda

conda create -n py38 python=3.8

conda env list

conda activate py38
```

#### dokcer



#### zsh

```bash
# git
brew install git

# autojump
brew install autojump

# markdown
brew install --cask qlmarkdown
brew install --cask qlimagesize mdimagesizemdimporter

# zsh-autosuggestion，用于命令建议和补全
cd ~/.oh-my-zsh/custom/plugins/
git clone https://github.com/zsh-users/zsh-autosuggestions
vi ~/.zshrc
plugins=(
  git
  zsh-autosuggestion
)

```







