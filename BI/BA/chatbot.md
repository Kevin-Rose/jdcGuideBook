

# Chat bot AI+BI的分析

[TOC]

------



## 1. **现状**

人工线下标注数据，

人工线下分析数据，

人工线下展示数据，

费用成本平台（约￥5000/month），人工成本高()

## 2.  阶段规划与价值

- 第一期：**实现系统自动展示**，人工线下标注数据，人工线下分析数据

- 第二期：**实现系统自动展示，实现人工线上标注数据**，人工线下分析数据

- 第三期：**实现系统自动展示，实现人工线上标注数据，机器线上分析数据**（系统预处理分析，人工核对抽查）

##   3. 规划内容

### 3.1 支持用户线上标注基础数据

- 业务价值点：   >>节省基础数据处理的时间，可以多人同时进行标注，简化标注的操作步骤，提高数据标注的效率，

### 3.2  报告的整体内容总结，

- 业务价值点： >>文字描述整体趋势，核心数据点展示，让用户具有全局观

  示意图

  <img src="D:\sourcecode\opensource\jdcGuideBook\images\image-20210506144308576.png" alt="image-20210506144308576" style="zoom: 33%;" />

### 3.3 基础数据Rawdata处理

   人工标注的数据格式如下：

   <img src="C:\Users\KevinLiu\AppData\Roaming\Typora\typora-user-images\image-20210506143305430.png" alt="image-20210506143305430" style="zoom:67%;" />

   

 ### 3.4根据用户问题定位真实意图(三期)

   -  业务价值:>>用户问的财务问题，比如“发票报销”定位到了IT问题上且分数为0.9，业务层面不对
   - 目前都是人工核对,LUIS的意图识别混淆，需要识别真实的意图，

   基于历史标注的数据（问题和意图）训练一个模型，可以根据用户当前的问题，判断LUIS的意图是否正确

#### 3.4.1 会话量，应用，意图，用户数量的展示

   ![image-20210514145532254](C:\Users\KevinLiu\AppData\Roaming\Typora\typora-user-images\image-20210514145532254.png)

 ### 3.5 **日报**

   - Active Users：相对当月过去时间新增的用户基础
   - Conversations：当天所有人新增的会话量
   - Bizconf Booked： 人工标注的   /从机，器人回复的话来判断“诺诺已经成功预定”
   - IT Reported：根据机器人的回复过滤“IT问题已送达”
   - via Click  via Chat： 不用
   - 日报明细展示

| Date      | Active Users+ | Conversations | Resolution Rate | Bizconf Booked | IT Reported | via Click | via Chat | IT     Right | Fin     Right |
| --------- | ------------- | ------------- | --------------- | -------------- | ----------- | --------- | -------- | ------------ | ------------- |
| 2021/4/1  | 57            | 177           | 90.63%          | 17             | 1           | 13        | 164      | 55           | 32            |
| 2021/4/2  | 37            | 121           | 83.10%          | 4              | 2           | 7         | 114      | 46           | 13            |
| 2021/4/3  | 11            | 37            | 92.00%          | 0              | 0           | 12        | 25       | 21           | 2             |
| 2021/4/4  | 7             | 17            | 78.57%          | 1              | 0           | 1         | 16       | 9            | 2             |
| 2021/4/9  | 31            | 200           | 89.52%          | 22             | 2           | 11        | 189      | 68           | 26            |
| 2021/4/5  | 18            | 71            | 91.67%          | 8              | 0           | 8         | 63       | 30           | 2             |
| 2021/4/6  | 81            | 323           | 91.16%          | 22             | 12          | 36        | 287      | 141          | 23            |
| 2021/4/7  | 52            | 273           | 84.62%          | 34             | 7           | 30        | 243      | 92           | 18            |
| 2021/4/8  | 29            | 188           | 82.02%          | 18             | 5           | 14        | 174      | 60           | 13            |
| 2021/4/10 | 17            | 97            | 83.08%          | 3              | 2           | 12        | 85       | 48           | 6             |

 - 日报趋势展示

![image-20210506150759962](C:\Users\KevinLiu\AppData\Roaming\Typora\typora-user-images\image-20210506150759962.png)

 ### 3.6 月报


![image-20210508175821016](C:\Users\KevinLiu\AppData\Roaming\Typora\typora-user-images\image-20210508175821016.png)

 <img src="C:\Users\KevinLiu\AppData\Roaming\Typora\typora-user-images\image-20210506144714119.png" alt="image-20210506144714119" style="zoom: 80%;" />

 <img src="C:\Users\KevinLiu\AppData\Roaming\Typora\typora-user-images\image-20210506144736445.png" alt="image-20210506144736445" style="zoom: 80%;" />

   <img src="D:\sourcecode\opensource\jdcGuideBook\images\image-20210506141609419.png" style="zoom: 80%;" />

 ### 3.7 支持时间的分析
   - 业务价值点：分析处理bot在工作时间和非工作时间的处理情况，
   - 支持年度/月度/应用维度查看，
   - 需要准备假期的日历

   ![image-20210506142643465](C:\Users\KevinLiu\AppData\Roaming\Typora\typora-user-images\image-20210506142643465.png)

 ### 3.8 月度的非工作时间的趋势

   业务价值点：

   ![image-20210506142705570](C:\Users\KevinLiu\AppData\Roaming\Typora\typora-user-images\image-20210506142705570.png)

### 3.9  小时会话量的趋势

业务价值点：知道每天的高峰和低峰时间点，合理安排人手，

支持维度：年/月/日

![image-20210506142734127](C:\Users\KevinLiu\AppData\Roaming\Typora\typora-user-images\image-20210506142734127.png)

--------------------------

### 3.10 有效性分析

- 业务价值点：>>验证bot解答机器人的业务问题后，2天内是否还会咨询同意意图的问题

![image-20210506143145150](D:\sourcecode\jdcGuideBook\images\image-20210506143145150.png)


​    

![image-20210506145009859](C:\Users\KevinLiu\AppData\Roaming\Typora\typora-user-images\image-20210506145009859.png)

![image-20210506152058924](C:\Users\KevinLiu\AppData\Roaming\Typora\typora-user-images\image-20210506152058924.png)

### 3.11 用戶使用排名

清楚知道每个月用户的月度访问天数/年度访问天数

![image-20210506142833595](C:\Users\KevinLiu\AppData\Roaming\Typora\typora-user-images\image-20210506142833595.png)

### 3.12 用户的词云图

    支持查看用户的年月日/应用维度的热词

### 3.13 新用户关心的应用、意图

​     可以看出哪些业务系统用户不熟悉

​     哪些意图用户不熟悉，

​     是不是培训不到位

### 3.14 用户的粘性度，应用或者意图的粘性度分析



### 3.15  基础用户的地理位置的分析

​     哪些大区，哪些部门的访问量比较高，哪些比较低

### 3.16  个性化的消息推送

对应的

### 3.17  应用和remedy的比较

目前的意图和应用系统的匹配，Remedy的Case的统计，比如Remedy的某些应用的模块Case减少了，

是不是用户都来诺诺里面解决了。

### 3.18 LUIS的应用与应用系统的关系

目前意图都是按照LUIS的应用，怎么去映射到业务系统上面去，比如AMS，OCE



- hour 小时

- day 天

- week 周

- month 月

## 4. 方案选项

1.数据安全 





"SN"	"ID"	"User ID"	"User Name"	"Question"	"Created Date"	"Created Time"	"Application ID"	"Application Name"	"Intent Name"	"Answer 8"	"Answer 7"	"Intent Score"	"Answer 6"	"Answer 5"	"Answer 4"	"Answer 3"	"Answer 2"	"Answer 1"
"189721"	"enterprisewechat|XHD|2020-01-01|00:47:28"	"enterprisewechat|XHD"	"邓旭浩"	"费用限额"	"2020-01-01"	"00:47:28"	"4aaab16c-81c7-4aa7-89c1-2b711de5df10"	"FIN_01"	"标准_费用标准"	\N	\N	"0.865329"	\N	\N	\N	\N	\N	\N

