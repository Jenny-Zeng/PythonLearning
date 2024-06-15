在做接口测试时，大量的数据返回格式都是Json格式，而Json格式很容易转换成字典的格式，因此熟悉字典的操作方法，是做接口测试的必备条件。

# 字典
先回顾下字典的基本操作
```Python
dict = {'name':'zeng','age':20,'love':['read、run'],'study':[{'time':'2014年','school':'巢湖'},{'time':'2018年','school':'沈阳'}]}
print(type(dict))
print(dict['name']) # 当key不存在时会报错：KeyError
print(dict.get('name1')) # 当key不存在时会返回None
# 链式表达
print(dict.get('study')[0]) #{'time': '2014年', 'school': '巢湖'}
print(dict.get('study')[0].get('school')) # 巢湖
# 获取字典的key、value、字典中每一个key和value
print(dict.values())
print(dict.keys())
print(dict.items())

# 字典的增加
dict1 = {}
dict1['name'] = 'Jenny'
print(dict1) # {'name': 'Jenny'}
# 字典的修改
dict1['name'] = 'Jack'
print(dict1) #{'name': 'Jack'}
# 字典的删除
print(dict1.pop('name'))
print(dict1) # {}
```
# 接口测试的数据类型Json
Json是一种轻量级的数据交互格式，是一种跨编程语言的，能够在不同编程语言中进行沟通和交互的标准数据格式。需要注意以下几点：
- Json 不是编程语言，是一种纯字符数据。
- Json 键值对的键部分，必须用双引号包裹，如果使用单引号，则无法转换成Json格式。

# dict与Json间的转换
- dict -> Json 使用 json.dumps()方法
- Json -> dict 使用 json.loads()方法
```Python
import json
dict = {"name":'zeng',"age":20,"love":['read','run'],"study":[{"time":'2014年',"school":'巢湖'},{"time":'2018年',"school":'沈阳'}]}
# 将字典转换成json格式，json格式实际上是一个字符串
dict_json = json.dumps(dict)
print(type(dict_json)) # <class 'str'>
print(dict_json) #{"name": "zeng", "age": 20, "love": ["read", "run"], "study": [{"time": "2014\u5e74", "school": "\u5de2\u6e56"}, {"time": "2018\u5e74", "school": "\u6c88\u9633"}]}
# 将json格式转换成字典
dict_new = json.loads(dict_json)
print(type(dict_new)) # <class 'dict'>
print(dict_new) # {'name': 'zeng', 'age': 20, 'love': ['read', 'run'], 'study': [{'time': '2014年', 'school': '巢湖'}, {'time': '2018年', 'school': '沈阳'}]
```
# 将Json中的数据取出来存储为csv文件
创建一个空列表 new_list，然后遍历 json_data 字典中的值，将其追加到 new_list 中。接下来，我们使用 pandas.DataFrame 创建一个数据框，并为其列命名为 'name'、'mos' 和 'code'。最后，我们使用 df.to_csv() 将数据框保存为 CSV 文件（此处命名为 demojson.csv）
```Python
#coding:utf-8
import pandas 
json_data = {
"01":[
{
"name":"zeng01",
"mos":"8",
"code":"200"
},
{"name":"zeng011",
"mos":"8",
"code":"201"}
],
"02":[
{
"name":"zeng02",
"mos":"8",
"code":"200"
},
{"name":"zeng022",
"mos":"8",
"code":"201"}
]
}
if __name__ == "__main__":
   
    newList = []
    for value in json_data.values():
        newList = newList+value
        pd=pandas.DataFrame(newList)
        pd.columns = ['name','mos','code']
        pd.to_csv("demojson.csv",index=False)
```