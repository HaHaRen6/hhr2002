---
title: "配置 Linux 服务器"
date: 2025-3-17
draft: false
# series: ["x"]
# series_order: 1
tags: ["Linux"]
---

## tmux

### 安装

`chmod -R +x <folder>`

#### 插件

- tpm(Tmux Plugin Manager)

  - [tmux-plugins/tpm: Tmux Plugin Manager](https://github.com/tmux-plugins/tpm)

  - ```
    git clone https://github.com/tmux-plugins/tpm ~/.tmux/plugins/tpm
    ```

  - ```
    # type this in terminal if tmux is already running
    tmux source ~/.tmux.conf
    ```

- TODO

### 使用

可修改`<prefix>`，我设置为 `Ctrl+a`

![Tmux简明教程| Dennis' Blog](https://images.lrl52.top/i/2023/07/27/5a861515-0.png)

#### 会话管理

> 一般只用保留一个session

| 快捷键                                 | 功能描述                     |
| ------------------------------------- | ---------------------------- |
| `tmux new -s <name>` or `tn`          | 创建命名会话                 |
| `<prefix> $`                          | 重命名当前会话               |
| `<prefix> d`                          | 分离当前会话（后台保持运行） |
| `tmux ls` or `tl`                     | 列出所有会话                 |
| `tmux attach -t <name>` or `ta`       | 重新连接指定会话             |
| `<prefix> s`                          | 可视化选择并切换会话         |
| `tmux kill-session -t <name>` or `tk` | 终止指定会话                 |

其中 `tn` `ta` `tl` `tk` 为zsh alias

#### 窗口管理

| 快捷键         | 功能描述               |
| -------------- | ---------------------- |
| `<prefix> c`   | 创建新窗口             |
| `<prefix> ,`   | 重命名当前窗口         |
| `<prefix> &`   | 关闭当前窗口           |
| `<prefix> 0-9` | 快速跳转到指定编号窗口 |
| `<prefix> p`   | 切换到上一个窗口       |
| `<prefix> n`   | 切换到下一个窗口       |
| `<prefix> l`   | 在最近使用的窗口间切换 |

####  面板操作

| 快捷键                 | 功能描述            |
| ---------------------- | ------------------- |
| `<prefix> %`           | 垂直分割面板        |
| `<prefix> "`           | 水平分割面板        |
| `<prefix> 方向键`      | 切换面板焦点        |
| `<prefix> z`           | 最大化/恢复当前面板 |
| `<prefix> x`           | 关闭当前面板        |
| `<prefix> Ctrl+方向键` | 调整面板大小        |
| `<prefix> Space`       | 切换面板布局        |

#### 小连招

```shell
tn work
tl
ta work
```

### 常见问题

设置不生效

```shell
tmux kill-server
```

## zsh

> 在非root用户的Linux下安装zsh（Linux中无zsh的情况下）

### 安装

[Linux 以非root用户安装zsh&配置on my zsh - Xi-iX - 博客园](https://www.cnblogs.com/XiiX/p/14618799.html)

在 `~/.bash_profile` 中添加下面这句保证ssh启动时自动切换为zsh

在 `~/.bashrc` 中添加下面这句保证vscode通过ssh启动时自动切换为zsh

// 不知道为啥，但是这么做有用

```shell
[ -f $HOME/config/zsh/bin/zsh ] && exec $HOME/config/zsh/bin/zsh -l
```

### 插件

```shell
plugins=(
        git
        z
        pip
        zsh-autosuggestions
        last-working-dir # 记录上一次退出命令行时候的所在路径
        zsh-syntax-highlighting
        extract # 解压
        copypath
        copyfile
        )
```

zsh-autosuggestions安装：

```bash
git clone https://github.com/zsh-users/zsh-autosuggestions ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-autosuggestions
```

zsh-syntax-highlighting安装：

```bash
git clone https://github.com/zsh-users/zsh-syntax-highlighting.git ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-syntax-highlighting
```

### 问题

```shell
echo $SHELL
/bin/bash
```

不知道如何解决

## conda

### 问题

疑似因为在非root用户的Linux下安装zsh（Linux中无zsh的情况下），导致

```shell
echo $SHELL
/bin/bash
```

从而conda安装脚本识别了错误了shell。

尝试过zsh miniconda-xxx.sh，但是报错。

### 解决

> 只能算临时解决方案

将 `~/.bashrc` 中的这一段放在 `~/.zshrc` 中（不要直接复制我的，里面路径不一样）

```shell
# >>> conda initialize >>>
# !! Contents within this block are managed by 'conda init' !!
__conda_setup="$('/home/huhaoran/miniconda3/bin/conda' 'shell.bash' 'hook' 2> /dev/null)"
if [ $? -eq 0 ]; then
    eval "$__conda_setup"
else
    if [ -f "/home/huhaoran/miniconda3/etc/profile.d/conda.sh" ]; then
        . "/home/huhaoran/miniconda3/etc/profile.d/conda.sh"
    else
        export PATH="/home/huhaoran/miniconda3/bin:$PATH"
    fi
fi
unset __conda_setup
# <<< conda initialize <<<
```

