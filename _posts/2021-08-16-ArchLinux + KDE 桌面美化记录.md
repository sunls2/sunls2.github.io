---
layout: mypost
title: Arch Linux + KDE 桌面美化记录
categories: [Arch,KDE,Theme]
---

## 先放效果图 😆

![koncolse](2021-08-16_13-44.png)

![dolphin](2021-08-16_13-44_1.png)

![goland](2021-08-16_17-03.png)

![vscode](2021-08-16_20-58.png)

![chrome](2021-08-16_13-45.png)

## 主题 🤡

### kvantum 主题

首先安装 `kvantum-qt5` 包，使用 `yay` 进行安装，此包是 `community` 下的包，也可以使用 `pacman` 进行安装：

```shell
# sudo pacman -S kvantum-qt5
yay -S kvantum-qt5
```

然后打开软件点击 `Change/Delete Theme`，在下拉框中选择 `AdaptNokto`，点击 `Use this theme` 使用这个主题。

（`AdaptNokto` 需要安装完下面的全局主题 `adapta-kde-git` 后才会出现）

### 全局主题

全局主题使用的也是 `adapta`，同样使用 `yay` 进行安装。（试了很多主题最喜欢这个！）
```shell
# 此包是aur的包，不能使用pacman安装
yay -S adapta-kde-git
```

plasma 样式、窗口装饰、欢迎屏幕都选择 `adapta`，颜色选择 `adapta nokto`，应用程序风格选择 `kvantum`，重启一下，搞定！🎉

### Goland 主题

`Goland` 使用的是 `Material Theme UI` 这个插件，直接在插件中心搜索下载，然后在设置中选择 `Atom One Dark` 主题。

`Material` 这个主题去除了边框间的一些线，让整个编辑器看起来更加统一，很有质感，非常 nice 🍻

### VSCode 主题

`VSCode` 同样也使用 `Atom One Dark` 这个主题，在扩展中直接搜索安装。效果同样很 nice 👏

## 图标 👾

图标使用的是 `papirus`，这个图标包是真的好看，覆盖的也很全，yyds！

貌似和 `adapta` 是同一个 team 开发的：https://github.com/PapirusDevelopmentTeam

````shell
# sudo pacman -S papirus-icon-theme
yay -S papirus-icon-theme
````

安装好之后在系统设置（外观=>图标）中选择 `papirus-dark`。

## Dock 栏 ✨

Dock 栏使用 `latte-dock` 和 KDE 桌面比较契合，自定义配置很多。主要是好看 🎉

```shell
# sudo pacman -S latte-dock
yay -S latte-dock
```

