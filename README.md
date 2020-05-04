# 百度贴吧帖子备份

重新搞了个分支做交互式的

其实是源于 52pojie 某个网友的需求

<p align="left">
<img src="https://img.shields.io/badge/Python-3.x-brightgreen?style=flat-square">
<img src="https://img.shields.io/github/license/hui-shao/TiebaBackup?color=orange&style=flat-square">
<img src="https://img.shields.io/badge/Platform-Windows%20%20%7C%20Linux-blue.svg?longCache=true&style=flat-square">
</p>


---

## Features

- 输入贴吧名，自动爬取选定页码范围的帖子
- 筛选爬取精品贴

![](https://github.com/hui-shao/TiebaBackup/blob/online/demo.png)
![](https://github.com/hui-shao/TiebaBackup/blob/online/wx.jpg)


## 说明
- main.py  自动爬取指定贴吧、指定页码范围的帖子
- main_good.py  仅爬取精品区的帖子，其余同上
- main_manual.py  手动输入帖子id，支持批量

## How to use:

<hr>

#### 环境配置

**Linux:**

```bash
apt-get install python3 python3-pip
pip3 install -r requirements.txt
python3 main.py
```

**Windows:**

在[ 官网 ](https://www.python.org/downloads/)下载python3.6或以上版本

```cmd
pip install -r requirements.txt
python3 main.py
```

<br>

#### 参数说明

| Var name       | Value                | Type          | Description                                |
|:------------:  |:--------------------:|:-------------:|:-------------------------------------------|
| pids           | [12345678, 12345679] | list (int)    | 帖子 ID 列表  （仅用于 main_manual.py）        |
| overwrite      | 1 / **2**            | int           | 是否覆盖已备份的文件<br>1为跳过，2为覆盖，其他值交互     |
| copy           | 0 / **1**            | int           | 是否把备份好的文件拷贝到网站目录<br>0为否，1为是，其他值交互   |
| sckey          | "xxxxxxxxxxx"        | string        | 用于Server酱推送的Key，没有请留空<br>可以到 [这里](http://sc.ftqq.com/3.version) 获取   |
| lz             | True / False         | bool          | 是否使用“只看楼主”模式 |
| comment        | **True** / False     | bool          | 是否包含楼中楼（评论） |

<br>

#### 其他说明

- 在不同的平台下，需要注意 py 文件的 “换行符(Line-Ending)”：`CRLF(Windows) / LF(Unix)`

- 如需插入自定义html代码，请修改 `Init(pid, overwrite)` 函数中的 `Write()` 部分；如需添加网站资源文件，请修改该函数中 `shutil.copy()` 部分，并把文件放入程序目录下的 "resources" 文件夹

<br>

#### 部署自动化(Linux)

使用 `crontab -e` 创建自动化，表示每天 11:30 和 23:30 时执行备份。例如：

```bash
30 11,23 * * * "python3" "/root/tieba_backup/main_all.py" >> /root/log1.txt 2>&1
```

<br>

还可以配合如下规则，以此实现每周六自动删除日志：

```bash
0 23 * * 6 rm /root/log1.txt
```

<br>

~~另外建议 `vim .bashrc` , 注释掉其中的 `alias rm='rm -i'` 和 `alias cp='cp -i`，否则可能因为需要交互，导致程序暂停~~

<br>

## Change log:

---

#### 2020.03.09

1. 适配 批量模式(list + for)
2. 优化 控制台信息输出的内容
3. 优化 Server酱推送消息内容的排版
4. 修复一些Bug：
    - 删除3天前的备份文件时，因“目录非空，无法删除”而报错的问题
    - 程序运行目录与脚本文件所在目录不一致时，无法找到网页文件并复制的问题

#### 2020.03.06

1. 支持 自动拷贝备份文件（html）到网站目录
2. 为网页新增 icon 和 title ，可能缓解某些情况下卡顿的问题
3. 修复一些"小Bug"

#### 2020.03.05

1. 诞生