深浅拷贝只针对可变对象，可变对象其实是值引用地址是否改变。
# 说在前面
- 可变类型：变量对应的值可以修改，但是内存地址不会发生改变
常见的可变类型：list、dict、set
```Python
li = [1,2,3,4]
print("li原来的内存地址",id(li)) # li原来的内存地址 4561078464
li.append(5)
print("li现在的内存地址",id(li)) # li现在的内存地址 4561078464

dic = {"name":"zeng","age":18}
print(id(dic)) # 4430991360
dic["name"] = "hello"
print(id(dic)) # 4430991360

s1 = {1,2,3}
print(id(s1)) # 4363013920
s1.add(4)
print(id(s1)) # 4363013920

l1 = [1,2,3,4]
print("l1",l1)
l2 = l1
l1.append(5)
print("*************")
print("l1",l1) # l1 [1, 2, 3, 4, 5]
print("l2",l2) # l2 [1, 2, 3, 4, 5]
# 赋值等于完全共享资源，一个值的改变会完全被另一个值共享
```

- 不可变对象：存储空间保存的数据不允许被修改
```Python
'''
常见的不可变类型
1. 数值类型：int、bool、float、complex
2. 字符串：str
3. 元组 tuple
'''
# 赋值之后，地址全部不同
a = 1
print(id(a))
a = 2
print(id(a))

str1 = "hello"
print(id(str1))
str1 = "world"
print(id(str1))

tup = (1,2)
print(id(tup))
tup = (1,2,3)
print(id(tup))
```
# 浅拷贝
浅拷贝是数据半共享，即拷贝最外层的对象，内部元素只拷贝一个引用。
浅拷贝会创建新的对象，拷贝第一层的数据，嵌套层会指向原来的内存地址
```Python
import copy
li = [1,2,3,[4,5,6]]
li2 = copy.copy(li)
print("li",li) # li [1, 2, 3, [4, 5, 6]]
print("li2",li2) # li2 [1, 2, 3, [4, 5, 6]]
# 查看内存地址
print("li内存地址:",id(li)) # li内存地址: 4365928640
print("li2内存地址:",id(li2)) # li2内存地址: 4366987136
# 内存地址不一样，说明不是同一个对象

li.append(8)
print("li",li) # [1, 2, 3, [4, 5, 6], 8]
print("li2",li2) # [1, 2, 3, [4, 5, 6]]
# 往嵌套列表添加元素
li[3].append(7)
print("li",li) # [1, 2, 3, [4, 5, 6, 7], 8]
print("li2",li2) # [1, 2, 3, [4, 5, 6, 7]]

print("li[3]内存地址",id(li[3])) # li[3]内存地址 4324134848
print("li2[3]内存地址",id(li2[3])) # li2[3]内存地址 4324134848
# 外层的内存地址不同，但是内层的内存地址相同
# 优点：拷贝速度快，占用空间少，拷贝效率高
```
# 深拷贝
深拷贝数据完全不共享，外层的对象和内层的元素都拷贝了一遍
```Python
import copy
li = [1,2,3,[4,5,6]]
li2 = copy.deepcopy(li)
print("li",li)  # [1, 2, 3, [4, 5, 6]]
print("li2",li2) # [1, 2, 3, [4, 5, 6]]
# 查看内存地址
print("li内存地址:",id(li)) # li内存地址: 4457973952
print("li2内存地址:",id(li2)) # li2内存地址: 4459032448
li.append(8) 
print(li) # [1, 2, 3, [4, 5, 6], 8]
print(li2) # [1, 2, 3, [4, 5, 6]]
# 在嵌套列表里添加元素
li[3].append(7) 
print(li) # [1, 2, 3, [4, 5, 6, 7], 8]
print(li2) # [1, 2, 3, [4, 5, 6]]
print("li[3]内存地址:",id(li[3])) # li[3]内存地址: 4457975744
print("li2[3]内存地址:",id(li2[3])) # li2[3]内存地址: 4459032640
'''
深拷贝数据变化只影响自己本身，跟原来的对象没有关联
'''
```
