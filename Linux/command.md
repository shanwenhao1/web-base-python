# Linux常用命令

[]: 表示参数, 如[-a]
|: 表示或

## 权限相关

- su [用户名]: 切换用户


## 查找相关

- ls [-a | -l]:
    - 目录: 列出该目录下的所有子目录与文件
    - 文件: 列出文件名及其他信息
- pwd: 显示出当前工作目录的绝对路径
- find: 在文件树中查找文件
- [grep](https://www.cnblogs.com/fulucky/p/8023025.html) [参数(可选)] '搜寻字符串' 文件名: 强大的文本搜索工具


## 显示相关

- cat/tac [选项] 文件: 查看目标文件的内容
- more [选项] 文件: 显示文件内容, 每次显示一屏
- less [参数] 文件: less不同于more, 还允许向后浏览文件
- head [选项] 文件: 在屏幕上显示指定文件的开头若干行
- tail [选项] 文件: 用于显示指定文件的末尾, 不指定文件时, 作为输入信息进行处理, 常用于查看日志文件
 
## 创建或删除相关

- [touch](https://www.linuxidc.com/Linux/2018-02/150800.htm) [选项] [文件名]: 更改文档或目录的日期时间(
包含存取和更改时间), 或者创建新文件
- mkdir 目录名: 创建目录
- rm [] 目录名或文件名: 删除文件或目录, -r 删除目录  -f 删除文件
- rmdir 递归目录名: 删除目录
    - p: 递归删除目录, 如果删除后父目录为空则一并删除父目录, 示例: rm -r test/test

    
## 路径相关

- cd: 跳转到指定目录, cd ..表示跳转至上一级目录, cd - 返回最近访问目录并跳转

## 拷贝或转移相关

- cp [参数] 源文件或目录 目标文件或目录: 复制文件或目录, 示例: cp -r test/ newTest/
- mv [参数(可选)] 源文件或目录 目标文件或目录: 对文件或目录重命名, 或者将文件从一个目录移动到另一个目录中.

## 时间相关

- [date](https://www.cnblogs.com/hunttown/p/5470527.html): 显示时间, 可用时间戳格式显示, 示例: date +"%Y-%m-%d"
- [cal](https://blog.csdn.net/gxiaop/article/details/55014760) [参数][月份][年份]: 用于查询日历等时间信息


## 压缩相关

- zip/unzip: 压缩文件或目录
- tar [-cxtzjvf] 文件与目录.tar: 解压文件

## 系统相关

- uname [选项]: 电脑或操作系统的相关信息, 示例: uname -a

## 相关文章

- [Linux基本命令总结](https://blog.csdn.net/tao934798774/article/details/79491951)