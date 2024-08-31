# Exceptions(异常)
- 顾名思义，异常就是我们的编码中出错的事情
- 例如我在编辑器中输入这一段代码(故意错误)：

```python
#我故意漏掉了一个双引号
print("hello,world)
```
- 此时我们如果在终端运行这代码，编译器就会声明此为 **"syntax error"**,语法错误提示我们应该仔细检查代码中的错误

## Runtime Errors（运行时错误）
- 运行时错误是指由代码中的意外行为造成的错误，例如，我们本来的意图是想让用户输入一个数字，但他们输入的却是一个字符而由于用户的这个意外输入，我们程序所引发的错误.

**那么我们应如何修复我们代码中的这些潜在的错误呢？**

## try
- 在Python中, `try` 和 `except`是在出现问题之前测试用户输入的方法，例如如下代码：
```python 
try:
   x=int(input("What`s x?"))
   print(f"x is {x}")
except ValueError:
   print("x is not an integer")
```
现在，我们运行此代码时，输入`50`将会被接受，而输入`python`这类的字符串将会产生用户可见的错误，告知他们为什么不接受他们的输入
- 当然，这不是实现此代码的最佳方式，我们正在尝试执行两行代码，作为最佳实践，我们应该只`try`我们担心可能会失败的最少代码行，因为调整代码为：
```python 
try:
   x=int(input("What`s x?"))
except ValueError:
   print("x is not an integer")

print(f"x is {x}")
```
-这下我们可以“高枕无忧”了，但事实真的是这样的吗？如果我们运行上述代码，则会发现，我们面临了一个新的错误！一个`NameError`为`x 为定义 这是为什么呢？
- 事实上，如果你检查从右到左的 `x=int (input(Whats x?"))` 中的运算顺序，它会试图把一个字符串分配给一个整数，而这操作是不可能的，因此`x`永远不会被赋值.
- 我们可以如下方式调整代码：
```python 
try:
    x=int(input("What`s x?")
excepet ValueError:
    print("x is not an integer")
else:
    print(f"x is {x}")
```
- 但是我们注意到，如果用户输入错误了，我们只能结束我们的程序了，而我们的目的是引导用户输入直到正确.
```python
while True:
    try:
       x=int(intput("What`s x?"))
    except ValueError:
       print("x is not an integer")
    else:
        break

print(f"x is {x}")
```
-这样我们可以创造循环，如果用户提供了正确的输入，循环中断，然后打印用户输入.

> [!IMPORTANT]
> 封装也是编程语言的核心思想，因此，我们应该再次改进上述代码，使其封装成一个函数

-我们修改代码如下：
```python
def main():
    x=get_int() #python命名更习惯于蛇形命名法
    print(f"x is {x}")

def get_int():
    while True:
         try:
            x=int(input("What`s x?"))
         except ValueError:
             print("x is not an integer")
         else:
              break
    return x

main()
```
-当然，我们仍可以改进这个程序：
```python 
def main():
      x=get_int()
      print(f"x is {x}")

def get_int():
    while True:
         try:
            x=int(input("What`s  x?"))
         except ValueError:
            print("x is  not an integer")
         else:
             return x

main()
```
-这下`return`不仅会让我们跳出循环，而且还会返回一个值

-其实也可以把上述代码变得更紧凑些：
```python
def main():
    x=get_int()
    print(f"x is {x}")

def get_int():
    while True:
        try:
            return int(input("What`s x?"))
        except ValueError:
            print("x is not an integer")

main()
```
-如果你觉得每次不断的提醒用户，你的输入有问题，会让他们感到“不安”的话，接下来要讲的关键词或许适合你

## pass
-这是我们要新学的一个关键词，可以使我们的代码不会警告用户，而只是不断地让他们输入，直到正确：
```python
def main():
    x=get_int():
    print(f"x is {x}")

def get_int():
    while True:
        try:
           return int(input("What`s x?")
        except ValueError:
           pass

main()
```
> [!NOTE]
> 当然，两种形式的代码都没有高下之分，在某些情况下，你可能想要用户非常清楚正在产生什么错误，而另一些情况，你可能会决定只是想再次获取他们的输入.不同的情况分类讨论，清楚你想要的就好.

- 现在我们的代码只局限在了询问x的值，变成了所谓的“硬编码”，因此我们可以按如下方式改进：
```python
def main():
    x=get_int("What`s x?")
    print(f"x is {x}")

def get_int(prompt):
    while True:
         try:
             return int(input(prompt))
         except ValueError:
             pass
main()
```

**- 最后来个总结，不要想着一次性就写出完美的代码，代码中的错误是不可避免的，希望你能利用今天学到的这些知识来更好的改进你的代码，防止会遇到的错误！**