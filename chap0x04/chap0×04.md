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

- ☑️

  支持以下常见图片批处理功能的单独使用或组合使用

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

#### **任务一**

- 安装`imagemagick`和`shellcheck`，并用远程从本地上传需要的图片文件。

  ```shell
  sudo apt-get update
  sudo apt-get install -y shellcheck
  sudo apt-get install imagemagick
  ```

![contents_of_the_current_folder](pending_image/contents_of_the_current_folder.png)

- 编写任务一脚本task01.sh

![task01_sh](pending_image/task01_sh.png)

- 测试脚本结果

![Image_Processing_Test 01](pending_image/Image_Processing_Test 01.png)

![Image_Processing_Test 02 ](pending_image/Image_Processing_Test 02 .png)

#### **任务二**   [[查看实验结果]](task02 _lab_ report.md)

- 将所需文件下载到本地。

  ```shell
  wget "https://c4pr1c3.gitee.io/linuxsysadmin/exp/chap0x04/worldcupplayerinfo.tsv"
  ```

- 编写脚本

  ![task02_sh](pending_image/task02_sh.png)

- 测试脚本结果

  ![World_Cup_Athlete_Statistics](pending_image/World_Cup_Athlete_Statistics.png)

#### **任务三** [[查看实验结果]](task03_lab_report.md)

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

- 编写脚本和相关内容

  ![task03_sh](pending_image/task03_sh.png)

- 测试脚本结果,将收集到的数据整成txt文件保存下来

  ![web_data_collection_process](pending_image/web_data_collection_process.png)

  

## 过程中遇到的问题







## 参考资料









