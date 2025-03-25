+++
title = "GNOME配置"
date = 2025-03-25
+++

## 前言

圆圆用过很长时间
[Sway](https://github.com/swaywm/sway)，
兼容
[i3](https://github.com/i3/i3)
的Wayland混成器。
圆圆很喜欢它快速切换工作区的功能，但圆圆几乎没用到平铺式混成器的优点。

圆圆用Redox时发现很棒的DE
[COSMIC](https://github.com/pop-os/cosmic-epoch)，
但单核占用高，XWayland兼容不好，text-input同样只支持
[text-input-v3](https://wayland.app/protocols/text-input-unstable-v3)。

今天圆圆把显示管理器换成GDM，gnome-shell作为gdm的依赖安装。
圆圆突然想到GNOME切换工作区也很方便，于是用了这个以前几乎没用过的DE。

## 工作区快捷键

i3/Sway默认配置了10个工作区的快捷键，用Super+1至Super+0切换工作区1-10。

GNOME只有4个工作区，首先应该增加工作区数量（其实圆圆最后才弄这步）：

```console
$ gsettings set org.gnome.desktop.wm.preferences num-workspaces 10
```

Super+1至Super+9被用作快速切换应用了，删掉这些按键绑定并设置新的：

```nu
1..9 | each {|n|
    gsettings set org.gnome.shell.keybindings switch-to-application-($n) '[]'
    gsettings set org.gnome.desktop.wm.keybindings switch-to-workspace-($n) $"['<Super>($n)']"
}
```

Super+0没被占用，直接设置快捷键即可：

```console
$ gsettings set org.gnome.desktop.wm.keybindings switch-to-workspace-10 "['<Super>0']"
```

## 背景图片

GNOME可以为预设和暗色设置不同的背景图片：

```console
$ gsettings set org.gnome.desktop.background picture-uri ~/wallpaper.png
$ gsettings set org.gnome.desktop.background picture-uri-dark ~/wallpaper.png
```
