<!-- TOC -->

- [插件 Extentions](#插件-extentions)
    - [Markdown TOC](#markdown-toc)
    - [Paste Image](#paste-image)
    - [Markdown Preview Github Styling](#markdown-preview-github-styling)
    - [vscode-icons](#vscode-icons)
    - [Markdown Emoji](#markdown-emoji)
- [VS Code 中使用 Git 提交到 Github](#vs-code-中使用-git-提交到-github)

<!-- /TOC -->

## 插件 Extentions
### Markdown TOC
- 如果遇到问题，参考该[issue](https://github.com/AlanWalk/markdown-toc/issues/65)

### Paste Image
- 将图片复制到剪贴板后，快捷键: `Ctrl + Shift + v`
- 可对图片路径等进行配置

### Markdown Preview Github Styling
- Github 风格的 Markdown 预览效果
- 预览快捷键：`Ctrl + K` + `v`

### vscode-icons
- 改变vscode的文件图标

### Markdown Emoji
- 支持许多 Markdown Emoji，[Emoji 列表](./emoji.md)


## VS Code 中使用 Git 提交到 Github
1、下载 git 并配置

配置用户信息：
```
$ git config --global user.name "John Doe"
$ git config --global user.email johndoe@example.com
```
生成 SSH 公钥
```
$ ssh-keygen -t rsa -C "your_email@youremail.com"
```

生成的公钥在 `你的路径/.ssh/id_rsa.pub`

把公钥 id_rsa.pub 的内容复制到 Github "Account settings" 的 SSH Keys 中即可。

2、在 Github 上新建一个仓库，并将该仓库 `git clone` 下来

3、在 vs code 中的操作

`Stage changes` --> 输入 `Message` --> `Push`

