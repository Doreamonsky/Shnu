# Shnu-Python

## Cas 登陆

> 由 'Shnu-cas.py 实现' 
> 已经实现通过Shnu cas登陆 course.shnu.edu.cn

在Cas登陆成功后，会得到Cookie CASTGC:TGT-XXX-cas

利用这个Cookie 就可以为所欲为了。

Cookie JSESSIONID 是当前的session ，也比较重要的。

## 课程爬虫

>  由 'Shnu-course-downlaoder.py 实现' 

下载的数据位于 data文件夹下

### 数据例子

> 120131101401.01$建筑力学$专业基础课程$班级:2017工程管理本科1班$彭丽，79$87$2$45/3$1-15$彭丽 星期一 4-4 [1-13]单  奉贤3教楼312  <br>彭丽 星期一 3-3 [1-15]单  奉贤3教楼312  <br>彭丽 星期二 8-9 [1-15]  奉贤3教楼512     

注意：我们使用的分隔符为 $

| 课程序号            | 课程名称 | 课程类别   | 教学班             | 教师  | 实际  | 上限  | 学分  | 学时/周 | 上课地点                                                                                            |
| --------------- | ---- | ------ | --------------- | --- | --- | --- | --- | ---- | ----------------------------------------------------------------------------------------------- |
| 120131101401.01 | 建筑力学 | 专业基础课程 | 班级:2017工程管理本科1班 | 彭丽  | 79  | 87  | 2   | 45/3 | 彭丽 星期一 4-4 [1-13]单  奉贤3教楼312  <br>彭丽 星期一 3-3 [1-15]单  奉贤3教楼312  <br>彭丽 星期二 8-9 [1-15]  奉贤3教楼512 |

# 课程数据API系统

我对与抓取的数据进行了重解析，并制作了uwsgi服务器。运行命令: uwsgi app.ini 

## 请求参数

| 请求参数 | 请求内容                          |
| ---- | ----------------------------- |
| json | {'request':类型,'keywords':关键词} |

类型有： 

courses_by_keywords 教学班课程 关键词用 , 分割 如2017,工程管理,1班

courses_by_classroom_keywords 教室 最好一次只询问一个 

注：运行 Shnu_exporter.py 来获得教学楼数据 进行本地保存

courses_by_id 课程序号 用 , 分割 如11111.11,22222.22

返回的统一为一张课程表的Json，需要自己进行单双周过滤与双，三，四连在一起的课程合并。

## 我的服务器

> 地址： https://waroftanks.cn/py/ 仅支持Get请求

## 课程表解析

> 由Shnu_course.py 类实现

### 关键词搜教学班课程表

> 由Shnu_course_table.py 实现

### 课程数组生成课程表

> 由Shnu_course_table_by_id.py 实现

### 教室课程表

> 由Shnu_ckassroom.py 实现
