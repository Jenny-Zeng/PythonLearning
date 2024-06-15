文件就是存储在某种长期存储设备上的一段数据,文件处理诸如对文本文件、图片等文件的处理，在Python中使用内置方法open()函数。
- 文件对象的方法：
    - open(file)：创建一个file对象，默认是以只读模式打开
    - read(n)：n表示从文件中读取的数据的长度，没有传n值就默认一次性读取文件的所有内容
    - write()将指定内容写入文件
    - close()：关闭文件

- 属性
    - 文件名.name：返回要打开的文件的文件名，可以包含文件的具体路径
    - 文件名.mode：返回文件的访问模式
    - 文件名.closed：检测文件是否关闭，关闭就返回True

```python
f = open('filedemo.txt')
print(f.name) #filedemo.txt
print(f.mode) # 文件访问模式 r 只读模式
f.close()
print(f.closed) #  True
```

# 读写操作

```python
f = open('filedemo.txt')
print(f.name) #filedemo.txt
print(f.mode) # 文件访问模式 r 只读模式
print(f.read()) # 打印出所有内容
f.close()
print(f.closed) #  True

# readline():一次读取一行内容，方法执行完，会把文件指针移动到下一行，准备再次读取
print(f.readline())

#一行一行读取
while True:
    text = f.readline()
    if not text:
        break
    print(text)

for i in f:
	print(i)
	text = f.readline()
	if not text:
		break
		
		
	#readlines():按照行的方式把文件内容一次性读取，返回的是一个列表，每一行的数据就是列表中的一个元素
f = open('filedemo.txt')
lines = f.readlines()
print(lines) # 打印出所有内容
f.close()
print(f.closed) #  True

#['hello world\n', 'hello world\n', 'hello world\n', 'hello world\n', 'hello world\n', 'hello world\n', 'hello world\n', 'hello world\n', 'hello world\n', 'hello world']
f = open('filedemo.txt')
for i in f.readlines():
    print(i)
f.close()
print(f.closed) #  True
```

访问模式：

| 模式 | 可做操作 |若文件不存在|是否覆盖|
| --- | --- |--- | --- |
| r| 只读 |报错 | - |
| r+ | 可读可写 |报错 | 是 |
| w | 只写 | 创建 |是  |
| w+| 可读可写 | 创建| 是 |
|a | 只写 | 创建|否，追加写  |
| a+| 可读可写 |创建 | 否，追加写 |

```python
'''
w 只写模式，文件存在就会先清空文件内容，再写入添加内容，不存在就创建新文件
'''
f = open('filedemo01.txt','w')
f.write("hello zeng") 
f.close()
print(f.closed) #  True

'''
+：表示可以同时读写某个文件
使用+会影响文件的读写效率，开发过程中更多时候会以只读、只写的方式才操作文件
r+：可读写文件，文件不存在就会报错
w+：先写再读，文件存在就重新编辑文件，不存在就创建新文件
'''
f = open('filedemo02.txt','w+')

'''
a:追加模式，不存在就创建新文件进行写入，存在则在原有内容的基础上追加新的内容
'''
f = open('filedemo02.txt','a')
f.write("\nhello zeng")
'''
文件光标就是文件指针，标记从哪个位置开始读取数据
文件定位操作
tell()：显示文件内当前位置，即文件指针当前位置
seek(offset,whence):移动文件读取指针到指定位置
offset：偏移量，表示要移动的字节数
whence：起始位置，表示移动字节的参考位置，默认是0，
	0代表文件开头作为参考位置，
	1代表当前位置作为参考位置，
	2代表将文件结尾代表参考位置
seek(0,0) 就会把文件指针移到文件开头
'''
f = open('filedemo02.txt','w+')
f.write("\nhello zeng")
pos = f.tell()
print(pos) # 11
f.seek(0,0)  # 文件指针移到文件开头
pos1 = f.tell()
print(pos1) # 0
f.close()
print(f.closed) #  True

#光标后有内容 才可以读数据
```
## with open用法

```python
'''
with open 作用：代码执行完，系统会自动调用f.close(),可以省略文件关闭步骤
'''
with open('filedemo02.txt','w') as f:
    f.write("我")

```

# 编码格式

注意：file对象的encoding参数的默认值与平台与关，比如windows上默认字符编码为GBK。
encoding表示编码集，根据文件的实际保存编码进行获取数据，更多的使用utf-8。

```python
# 如果出现乱码问题，加入参数：encoding='utf-8'
with open('filedemo02.txt','w',encoding='utf-8') as f:
    f.write("我")
    
'''
案例：图片复制 需要加一个'b'
读取图片，图片是一个二进制文件
'''

with open('Desktop/20190923074046969.jpg','rb') as f:
    img = f.read()
    print(img)
# 将读取到的内容写入到当前文件中
with open('demo.jpg','wb') as file:
    file.write(img)
```

# 目录常用操作
```Python
import os
# 1. 文件重命名，os.rename(旧名字，新名字)
os.rename("demo01.jpg","demo.jpg")
# 2.移除文件
os.remove("filedemo.txt")
# 3.创建文件夹
os.mkdir("zeng")
os.mkdir("zeng01")
# 4. 删除文件夹
os.rmdir("zeng01")
# 5. 获取当前目录
print(os.getcwd())
# 获取目录列表
print(os.listdir())
```
## 从Excel中过滤数据转换成列表、字典
```Python
#coding:utf-8
import pandas 
df = pandas.read_csv("demojson.csv")
name,mos,code = [],[],[]
for i in df.index.values:
    # 按行读取，并把每行内容转换成一个字典
    row = df.loc[i].to_dict()
    # 将每一行转换成字典后添加到列表
    name.append(row.get('name'))
    mos.append(row.get('mos'))
    code.append(row.get('code'))
    print({"name":name,"mos":mos,"code":code})
'''
结果：
{'name': ['zeng01'], 'mos': [8], 'code': [200]}
{'name': ['zeng01', 'zeng011'], 'mos': [8, 8], 'code': [200, 201]}
{'name': ['zeng01', 'zeng011', 'zeng02'], 'mos': [8, 8, 8], 'code': [200, 201, 200]}
{'name': ['zeng01', 'zeng011', 'zeng02', 'zeng022'], 'mos': [8, 8, 8, 8], 'code': [200, 201, 200, 201]}
'''
```