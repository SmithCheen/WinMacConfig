# Scoop

## 安装

```bash
Set-ExecutionPolicy RemoteSigned -Scope CurrentUser
irm get.scoop.sh | iex
scoop help
```

## 代理

```bash
scoop config proxy 127.0.0.1:7890
```

## 包

```bash
scoop install git
scoop bucket add extras
```

目录：https://rasa.github.io/scoop-directory/by-stars.html

## Java

```bash
scoop bucket add Java
scoop insatll openjdk8-redhat
scoop install openjdk17
```



