---
title: MacOS 中的 chflags 命令
date: 2024-04-19 01:49:54
tags: linux
---

在 macOS 中，我们可以使用 `chflags` 命令来更改文件或目录的标志（flags），从而控制它们的属性和行为。通过修改这些标志，我们可以隐藏文件、防止其被修改或删除，以及进行其他操作。以下是关于 `chflags` 命令的一些基本信息和示例用法。

### 语法

`chflags` 命令的基本语法如下：

```shell
chflags [-R] flags file...
```

其中：

- `-R`：可选参数，用于递归地应用标志到指定目录下的所有文件和子目录。
- `flags`：要设置的标志。
- `file...`：要操作的文件或目录。

### 常用标志

- `hidden`：将文件或目录标记为隐藏，使其在图形界面的 Finder 中不可见。
- `nohidden`：取消文件或目录的隐藏标记。
- `uchg`：防止文件被修改、重命名或删除，只有超级用户或文件的拥有者才能更改标志。
- `nouchg`：取消用户更改禁止标志。
- `schg`：防止文件被修改、重命名或删除，只有超级用户才能更改标志。
- `noschg`：取消系统更改禁止标志。

### 示例用法

1. 将文件设置为隐藏：
   ```shell
   sudo chflags hidden filename
   ```

2. 取消文件的隐藏标记：
   ```shell
   sudo chflags nohidden filename
   ```

3. 将目录及其所有内容设置为只读，防止修改、重命名和删除：
   ```shell
   chflags -R uchg directory
   ```

4. 将 hosts 文件锁定及解锁

   ```shell
   # 锁定文件
   sudo chflags uchg,schg /etc/hosts
   # 解锁文件
   sudo chflags nouchg,noschg /etc/hosts
   ```
5. 查看文件特殊标记

   ```shell
   ls -lO /etc/hosts
   
   # 显示如下
   -rw-r--r--@ 1 root  wheel  schg,uchg 2295  5 19 15:08 /etc/hosts
   ```

>  请注意，执行 `chflags` 命令可能需要超级用户权限（root）或适当的权限。在使用该命令时，请谨慎操作，并确保了解其影响和正确的使用方法。

### MacOS 软件已损坏

```bash
sudo xattr -r -d com.apple.quarantine  /Applications/xxx.app
```
