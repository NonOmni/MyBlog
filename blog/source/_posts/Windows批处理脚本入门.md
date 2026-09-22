---
title: Windows 批处理脚本入门
date: 2025-06-17
categories:
  - Windows
tags:
  - bat
  - 批处理
  - cmd
---

## 命令行

### cmd 与 PowerShell

cmd 是 PowerShell 的子集。

### 说明

- 不区分大小写
- 按上下键可以查看历史命令
- Tab 键可以自动补全
- 使用 `/?` 或 `/help` 可以查看命令用法，用法中的 `[]` 代表可选
- 命令基本格式：`命令 参数列表`

## 基本命令

| 命令    | 功能 | 举例          |
| ------- | ---- | ------------- |
| `echo`  | 显示 |               |
| `pause` | 暂停 | `pause > nul` |
| `cls`   | 清屏 |               |
| `exit`  | 退出 |               |

## 常用命令

| 命令       | 功能          | 举例                 |
| ---------- | ------------- | -------------------- |
| `type`     | 显示文件内容  | `type 1.txt`         |
| `find`     | 查找字符串    | `find "abc" 2.txt`   |
| `fc`       | 比较文件内容  | `fc 1.txt 2.txt`     |
| `date`     | 显示/修改日期 | `date /T`            |
| `time`     | 显示/修改时间 | `time /T`            |
| `ping`     | 网络连接测试  | `ping www.baidu.com` |
| `ipconfig` | TCP/IP 信息   |                      |
| `set /a`   | 计算表达式    | `set /a 6%4`         |
| `shutdown` | 关机          | `shutdown /s /t 60`  |

### 多命令

```bat
&  顺序执行多条命令，不管命令是否执行成功
&& 顺序执行多条命令，前面的命令错误则不执行后面的命令
|| 顺序执行多条命令，碰到执行正确的命令后将不执行后面的命令
abc & dir & bcd
abc && dir && bcd
abc || dir || bcd
```

### 重定向

```bat
>  输出重定向
>> 追加重定向
<  输入重定向
date /t > 1.txt
time /t >> 1.txt
find "/" < 1.txt
```

### 管道

```bat
| 前一个命令的输出作为后一个命令的输入
dir | find "txt"
```

## 文件操作命令

- 路径分隔符：`\`
- 当前目录：`.`
- 上一级目录：`..`

| 命令            | 功能               | 举例                           |
| --------------- | ------------------ | ------------------------------ |
| `dir`           | 显示文件夹内容     | `dir /A`                       |
| `tree`          | 显示文件夹树形结构 | `tree /F`                      |
| `盘符:`         | 进入指定磁盘       | `c:` `d:`                      |
| `cd`            | 切换目录           | `cd test` `cd ..`              |
| `mkdir` 或 `md` | 创建目录           | `mkdir test`                   |
| `rmdir` 或 `rd` | 删除目录           | `rmdir test`                   |
| `del`           | 删除文件           | `del 1.txt` `del /q/a/f *.txt` |
| `rename` 或 `ren` | 重命名           | `rename a.txt b.txt`           |
| `copy`          | 复制文件           | `copy a\1.txt b\1.txt`         |
| `move`          | 移动文件/重命名    | `move a\1.txt 2.txt`           |

## 批处理

### 基本结构

```bat
@echo off       # 关闭回显
......
pause           # 暂停。或 pause > nul
```

### 运行方式

- 双击运行
- 在 cmd 中运行（可以传参）

### 变量

```bat
# 设置变量
set 变量名=变量值
set /a 变量名=表达式
# 取消变量
set 变量名=
# 打印变量
set 变量名
# 列出变量
set
# 引用变量
%变量名%
# 输入变量值
set /p 变量名=提示文字
```

### 预定义的变量

| 变量名             | 值                               |
| ------------------ | -------------------------------- |
| `%cd%`             | 当前目录                         |
| `%date%`           | 当前日期                         |
| `%time%`           | 当前时间                         |
| `%random%`         | 0~32767 之间的随机数            |
| `%path%`           | 环境变量                         |
| `%errorlevel%`     | 上一个命令的返回值，0 表示执行成功 |
| `%0`、`%1`、`%2`…… | 参数。`%0` 表示命令名           |

### 调用

```bat
call 可执行文件 [参数列表]
```

### 条件

```bat
if [not] 条件 (
    语句块
) else (
    语句块
)
```

条件类型：

- `errorlevel number`：上一个程序的返回值大于等于 number 则为 true
- `string1==string2`：两个字符串匹配则为 true
- `exist filename`：文件名存在则为 true
- `[/I] string1 compare-op string2`：比较数值或字符串（`/I` 忽略大小写）
  - `equ` 等于
  - `neq` 不等于
  - `lss` 小于
  - `leq` 小于等于
  - `gtr` 大于
  - `geq` 大于等于
- `defined variable`：如果定义了该变量则为 true

### 跳转

```bat
goto label      # 跳转到标签所在行
:label          # 标签以冒号开头
```

### 循环

基本语法：

```bat
for %%i in (set) do (
    语句块
)

# 循环变量用 %% 指定，只能是单字母
# set 表示文件集合（也可以是空文件），元素之间以逗号或空格分隔，支持通配符

for %%i in (a,b,c) do (echo %%i)
for %%i in (*.*) do (echo %%i)
```

扩展语法：

- 只遍历文件夹

  ```bat
  for /d %%i in (set) do
  ```

- 遍历指定文件夹下的所有文件，不指定则表示当前目录。如果 set 为 `.` 表示枚举目录树

  ```bat
  for /r [[drive:]path] %%i in (set) do
  for /r %%i in (*) do (echo %%i)
  for /r d:\up %%i in (.) do (echo %%i)
  ```

- 遍历数字序列

  ```bat
  for /l %%i in (start,step,end) do
  ```

- 遍历文件内容

  ```bat
  for /f %%i in (file) do
  ```
