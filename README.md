## 描述

领域特定语言（Domain Specific Language，DSL）可以提供一种相对简单的文法，用于特定领域的业务流程定制。
本作业要求定义一个领域特定脚本语言，这个语言能够描述在线客服机器人
（机器人客服是目前提升客服效率的重要技术，在银行、通信和商务等领域的复杂信息系统中有广泛的应用）
的自动应答逻辑，并设计实现一个解释器解释执行这个脚本，可以根据用户的不同输入，根据脚本的逻辑设计给出相应的应答。

 

## 基本要求
- 脚本语言的语法可以自由定义，只要语义上满足描述客服机器人自动应答逻辑的要求。

- 程序输入输出形式不限，可以简化为纯命令行界面。

- 应该给出几种不同的脚本范例，对不同脚本范例解释器执行之后会有不同的行为表现。



## 评分标准
本作业考察学生规范编写代码、合理设计程序、解决工程问题等方面的综合能力。满分100分，具体评分标准如下：

- 风格：满分15分，其中代码注释6分，命名6分，其它3分。

- 设计和实现：满分30分，其中数据结构7分，模块划分7分，功能8分，文档8分。

- 接口：满分15分，其中程序间接口8分，人机接口7分。

- 测试：满分30分，测试桩15分，自动测试脚本15分

- 记法：满分10分，文档中对此脚本语言的语法的准确描述。

注意：抄袭或有意被抄袭均为0分



### 程序逻辑

运行脚本-输入语言-输出



### 服务内容

1. 投诉
2. 账单
3. 套餐
4. 余量 
5. 其他 失败

   1. 问候 您好-需求
   2. 终止 没有-感谢

| 实际 | 名称     | 结构                                                         |
| ---- | -------- | ------------------------------------------------------------ |
| 投诉 | complain | str arr                                                      |
| 账单 | bill     | int money, int traffic                                       |
| 套餐 | plan     | int money, int traffic enum[10,20,50] [24,48,120] [100,200,500] |
| 余量 | balance  | int money, int traffic                                       |

| Step            | 语音                             |
| --------------- | -------------------------------- |
| welcome         | 您好，这里是自助语音客服         |
| quest           | 请问，您有什么需求               |
| listen          | 【接收语音输入】（5-20秒）       |
| -------------   | welcome 和 recognize 自动跳转    |
| complain        | 您有什么要投诉的吗？             |
| bill            | 您的本月累计消费xx元，使用流量xxM，已通话xx分钟 |
| plan            | 您的套餐价为xx元每月，包含通话时间xx分钟，流量xxM |
| balance | 您的账户余额为xx元，剩余通话时间xx分钟，流量xxM |
| thanks | 感谢您的使用 |



```cpp
Step welcome
	Speak  "您好，这里是自助语音客服"
	Default quest
Step quest
    Speak "请问，您有什么需求吗"
    Listen 5, 20
	Branch "投诉", complainProc
	Branch "账单", billProc
    Branch "套餐", planproc
    Branch "余量", balanceproc
    Branch "没有", thanks
    Speak "您的需求不在服务范围内,您有其他需求吗"
    Default quest
Step complainProc
	Speak "您有什么要投诉的吗"
	Listen 5, 50
    Speak "感谢您的投诉，您的意见是我们改进工作的动力"
	Default quest
Step billProc
	Speak "您的本月累计消费xx元，使用流量xxM，已通话xx分钟"
	Default quest
Step planProc
	Speak "您的套餐为xx元每月，包含通话时间xx分钟，流量xxM"
	Default quest
Step balanceProc
    Speak "您的账户余额为xx元，剩余通话时间xx分钟，流量xxM"
	Default quest
Step thanks
	Speak "感谢您的来电，再见"
	Exit
```

### Interpreter

 

动作 

- 中文识别？？

语法树

- 变量表

parser

​	代码生成

interpreter

