---
layout:     post
title:      Markdown语法
subtitle:   工欲善其事，必先利其器。
date:       2020-02-06
author:     Rain
header-img: img/post-bg-map.jpg
catalog: true
tags:
    - 爬虫
---


我们在开发中常常需要利用一些假数据来做测试,这种时候就可以使用 Faker 来伪造数据从而用来测试.

## 安装

```shell
pip install Faker

```

## 使用

[官方文档](https://faker.readthedocs.io/en/master/)

### 使用工厂函数创建实例


```python3
from faker import Factory
fake = Factory.create()
```


### 使用Faker创建实例

```python3
from faker import Faker
fake = Faker()  # locale参数指定语言/地区如‘zh_CN’为中文,默认为英文

fake.name()

>>>'Audrey Robinson'
fake.address()
>>>'4266 Fritz Shore\nLewischester, AL 24594-7593'

fake.text()
>>>'Odio porro unde sint aliquid beatae. Ex officiis porro nostrum laboriosam deleniti nisi. A aut molestiae ratione ipsam perspiciatis facere.\nDicta incidunt at deleniti recusandae accusamus quisquam.'
```


## 常用方法
+ user_agent 用户代理
    + 可以指定UA的类别，如fake.chrome()指定为谷歌UA
+ address 地址
+ person 人物类：性别、姓名等
+ barcode 条码类
+ color 颜色类
+ company 公司类：公司名、公司email、公司名前缀等
+ credit_card 银行卡类：卡号、有效期、类型等
+ currency 货币
+ date_time 时间日期类：日期、年、月等
+ file 文件类：文件名、文件类型、文件扩展名等
+ internet 互联网类
+ job 工作
+ lorem 乱数假文
+ misc 杂项类
+ phone_number 手机号码类：手机号、运营商号段
+ python python数据
+ profile 人物描述信息：姓名、性别、地址、公司等
+ ssn 社会安全码(身份证号码)


## 自定义扩展
心有多大，大海就有多大

当Faker不能满足你的需求时, 可以利用自定义扩展，引用外部的 provider，自定义你要的功能。

```python3
from faker import Faker
fake = Faker()

# first, import a similar Provider or use the default one
from faker.providers import BaseProvider

# create new provider class
class MyProvider(BaseProvider):
    def foo(self):
        return 'bar'

# then add new provider to faker instance
fake.add_provider(MyProvider)

# now you can use:
print(fake.foo())
```

## 命令行集成

Faker提供了一个命令行工具，可以在shell或者其他程序中生成一些伪数据。
```shell
$ faker address
968 Bahringer Garden Apt. 722Kristinaland, NJ 09890

$ python3 -m faker address
432 Marvin Wells Apt. 593\nWest Eric, DC 45650-8420

$ faker -l de_DE address
Samira-Niemeier-Allee 5694812 Biedenkopf

$ faker profile
{'job': 'Designer, blown glass/stained glass', 'company': 'Dennis-Bowers', 'ssn': '034-28-9965', 'residence': '34796 Jeremiah Station Apt. 782\nWest Timothy, TX 24139-6974', 'current_location': (Decimal('-47.425017'), Decimal('-42.743615')), 'blood_group': '0+', 'website': ['https://www.gardner.biz/', 'http://glover-ellison.info/', 'http://www.harrison.biz/'], 'username': 'patrick33', 'name': 'Alexandra Montgomery', 'sex': 'F', 'address': '2314 Collier Stream Suite 093\nMcintyreside, UT 19553', 'mail': 'gomezterri@hotmail.com', 'birthdate': '2005-01-30'}

$ faker profile ssn,name
{'ssn': '344-68-7420', 'name': 'Veronica Brennan'}

$ faker -r=3 -s=";" name
Willam Kertzmann;
Josiah Maggio;
Gayla Schmitt;
```

### 命令行参数
```shell
faker [-h] [--version] [-o output]
      [-l {bg_BG,cs_CZ,...,zh_CN,zh_TW}]
      [-r REPEAT] [-s SEP]
      [-i {module.containing.custom_provider othermodule.containing.custom_provider}]
      [fake] [fake argument [fake argument ...]]
```

### 参数说明
- faker ： 在shell中，faker 命令也可以用 python -m faker 来代替
- -h，--help ： 帮助信息
- --version ：显示版本
- -o FILENAM ：输出结果到文件中
- -l {bg_BG,cs_CZ,...,zh_CN,zh_TW} ：指定本地化，zh_CN 表示中文
- -r REPEAT ：指定生成多少条相同类型的数据
- -s SEP ：在每个输出后边添加指定的分隔符
- -i {my.custom_provider other.custom_provider} ：自定义扩展，prividers列表。注意，这里要指定包含你 provider - 类的模块的路径，而不是程序本身。
- fake ：指定方法名称，如：name , address , text 等
- [fake argument ...] ：为方法指定参数。

**仅供学习交流使用，遵纪守法呀兄弟**

