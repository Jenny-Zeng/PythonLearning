# 条件语句
```Python
if 条件表达式1:
    语句块
elif 条件表达式2:
    语句块
else:
    语句块
```
另外需要知道一些运算符
- 比较运算符
```python
==  != > >= < <=
```
- 逻辑运算符

```python
and or not
```
- 三目运算（三元表达式）

# 循环语句
```Python
for i in range(10):
    print(i)

i = 0
while i < 10:
    i++
```
# break 和 continue 的区别
break 和 continue 是在循环结构中使用的关键字，用于控制循环的执行流程。

break 关键字用于立即终止循环，并跳出循环体。当代码执行到 break 语句时，循环会立即停止，并继续执行循环后的代码。break 可用于 for 循环和 while 循环。
以下是 break 的示例：
```Python
for i in range(5):
    if i == 3:
        break
    print(i)

# 输出：
# 0
# 1
# 2
```
在上述示例中，当 i 的值等于 3 时，break 语句被执行，循环立即终止。
continue 关键字用于跳过当前循环中的剩余代码，并进入下一次循环迭代。当代码执行到 continue 语句时，循环会跳过当前迭代中 continue 之后的代码，直接进行下一次循环迭代。continue 同样可用于 for 循环和 while 循环。

以下是 continue 的示例：
```Python
for i in range(5):
    if i == 3:
        continue
    print(i)

# 输出：
# 0
# 1
# 2
# 4
```
在上述示例中，当 i 的值等于 3 时，continue 语句被执行，跳过了该次循环迭代中 continue 之后的代码，然后继续进行下一次循环迭代。
因此，break 用于完全终止循环，而 continue 用于跳过当前迭代并继续下一次迭代。