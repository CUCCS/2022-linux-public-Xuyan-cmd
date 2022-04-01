# Linux网络与系统管理实验（四）shell脚本编程基础

------

## 实验环境

- **VirtualBox 6.1**
- **Ubuntu 20.04.02 Server 64bit**
- **Travis CI**
- **VsCode（已安装相应环境依赖）**

## 实验内容

### 任务一：用bash编写一个图片批处理脚本，实现以下功能：

- ☑️支持命令行参数方式使用不同功能

- ☑️支持对指定目录下所有支持格式的图片文件进行批处理指定目录进行批处理

- ☑️支持以下常见图片批处理功能的单独使用或组合使用

  - ☑️支持对jpeg格式图片进行图片质量压缩
  - ☑️支持对jpeg/png/svg格式图片在保持原始宽高比的前提下压缩分辨率
  - ☑️支持对图片批量添加自定义文本水印
  - ☑️支持批量重命名（统一添加文件名前缀或后缀，不影响原始文件扩展名）
  - ☑️支持将png/svg图片统一转换为jpg格式

### 任务二：用bash编写一个文本批处理脚本，对以下附件分别进行批量处理完成相应的数据统计任务：

- ☑️统计不同年龄区间范围（20岁以下、[20-30]、30岁以上）的球员数量、百分比
- ☑️统计不同场上位置的球员数量、百分比
- ☑️名字最长的球员是谁？名字最短的球员是谁？
- ☑️年龄最大的球员是谁？年龄最小的球员是谁？

### 任务三：用bash编写一个文本批处理脚本，对以下附件分别进行批量处理完成相应的数据统计任务：

- ☑️统计访问来源主机TOP 100和分别对应出现的总次数
- ☑️统计访问来源主机TOP 100 IP和分别对应出现的总次数
- ☑️统计最频繁被访问的URL TOP 100
- ☑️统计不同响应状态码的出现次数和对应百分比
- ☑️分别统计不同4XX状态码对应的TOP 10 URL和对应出现的总次数
- ☑️给定URL输出TOP 100访问来源主机

## 实验要求

- 所有源代码文件必须单独提交并提供详细的`-help`脚本内置帮助信息
- 任务三的所有统计数据结果要求写入独立实验报告

## 操作过程

#### **以下代码执行情况可查看**[我的Travis CI](https://app.travis-ci.com/github/CUCCS/2022-linux-public-Xuyan-cmd)

#### **任务一**

- 安装`imagemagick`和`shellcheck`，并用远程从本地上传需要的图片文件。

  ```shell
  sudo apt-get update
  sudo apt-get install -y shellcheck
  sudo apt-get install imagemagick
  ```

![contents_of_the_current_folder](pending_image/contents_of_the_current_folder.png)

- 编写任务一脚本[[task01.sh]](codefile/task1.sh)

![task01_sh](pending_image/task01_sh.png)

**测试结果**：

![taskone_part_one](pending_image/taskone_part_one.png)

![taskone_part_two](pending_image/taskone_part_two.png)

#### **任务二**  [[查看实验结果报告]](task02_lab_ report.md)

- 将所需文件下载到本地。

- ```shell
  wget "https://c4pr1c3.gitee.io/linuxsysadmin/exp/chap0x04/worldcupplayerinfo.tsv"
  ```
  
- 编写脚本[[task02.sh]](codefile/task2.sh)

  ![task02_sh](pending_image/task02_sh.png)

- 测试脚本结果

  ![World_Cup_Athlete_Statistics](pending_image/World_Cup_Athlete_Statistics.png)

#### **任务三** [[查看实验结果报告]](task03_lab_report.md)

- 提前安装`p7zip-full`

  ```shell
  sudo apt-get install p7zip-full
  ```

- 将所需文件下载到本地并解压

  ```shell
  wget "https://c4pr1c3.gitee.io/linuxsysadmin/exp/chap0x04/worldcupplayerinfo.tsv"
  7z x web_log.tsv.7z
  ```

​		![get_web_IP](pending_image/get_web_IP.png)

- 编写脚本和相关内容[[task03.sh]](codefile/task3.sh)

  ![task03_sh](pending_image/task03_sh.png)

- 测试脚本结果,将收集到的数据整成txt文件保存下来

  ![web_data_collection_process](pending_image/web_data_collection_process.png)

  

## 过程中遇到的问题

- 在作业仓库中部署Travis CI时编写的.travis.yml文件无法被识别和读取，Travis不能记录到我的相关代码活动

  **解决方法**：将.travis.yml文件放在当前分支下的根目录里面即可被Travis识别和执行。

- 在.travis.yml文件的编写中，根据我的文件目录结构cd进“chap0×04”，因为我的脚本在codefile/文件夹，所以我再要cd codefile/去运行我的脚本，但是我在这个yml文件编写过程中始终不能成功执行。

  **解决方法**：由于Travis CI不能识别“×”，因此不能够识别到我的作业文件夹，故通过git bash删除原文件夹重新命名，因为git bash不能区分乘号和小写拉丁字母x，所以用git rf的改名方法在此处没有效果。

- 在统计2014年世界杯运动员的相关姓名时，一些人名带有特殊符号，此时bash语法不清楚如何去读写识别、

  **解决方法**：通过shll的通配符去完成识别

- 任务二中，统计位置实验结果中 `Défenseur` 应为法语守门员写法，理论上应该归入`Defender` 。源数据问题未作调整。

- 任务一中，加水印本地正常运行，travis运行报错 `convert:unable to read font (null)`

  **解决方法**：有些系统没有默认安装字体库，搜集资料后增加安装 `ghostscript`。

## 参考资料

- [2021Linux系统与网络管理](https://www.bilibili.com/video/BV1Hb4y1R7FE?p=67)
- [shell脚本编程基础](https://c4pr1c3.github.io/LinuxSysAdmin/chap0x04.md.html#/title-slide)
- [How the bash shell recognizes special symbols](https://blog.csdn.net/woshaguayi/article/details/89365142)
- [Travis CI official documentation](https://docs.travis-ci.com/user/tutorial/?utm_source=help-page&utm_medium=travisweb)
- [How to delete specified files and directories in git](https://blog.csdn.net/shuilan0066/article/details/70568595)
- [How to use weget](https://www.jb51.net/LINUXjishu/86326.html)
- [CUCCS/Linux-2020-LyuLumos](https://github.com/CUCCS/linux-2020-LyuLumos)
- [Linux command--find and statistics (grep, awk, sort, uniq, wc)](https://blog.csdn.net/hshuihui/article/details/77915398)
- [Summary of shell interception string methods in linux](https://blog.51cto.com/u_13865122/2727802)
- [.TSV file extension meaning](https://www.reviversoft.com/zh-cn/file-extensions/tsv)
- [shell多进程处理多图像](https://blog.csdn.net/weixin_40805392/article/details/104792874)
- [Shell Tutorial](https://www.runoob.com/linux/linux-shell.html)
- [Extraction method of file suffix, directory, etc. in shell](https://blog.csdn.net/binggan_2019/article/details/89024460?ops_request_misc=&request_id=&biz_id=102&utm_medium=distribute.pc_search_result.none-task-blog-2~all~sobaiduweb~default-6)







