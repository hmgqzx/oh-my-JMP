微信开发的基本流程，先判断用户传入数据的类型MsgType，然后再获取用户输入的内容content,再对content进行处理，再返回给用户



Python 运行环境使用的是 Python 2.7.9。



预装的第三方模块列表：

MySQLdb

webpy

对于MySQLdb的使用，可以参考其 [官方文档](http://mysql-python.sourceforge.net/MySQLdb.html) 。



用 sublime 时，由于自动检查不够完善，万一修改过程中缩进出问题（有时难发现）



定时任务

[新浪云-定时任务](https://www.sinacloud.com/doc/sae/python/cron.html)



###  Memcached与KVDB的区别

Memcached将数据存储在内存中，数据易丢失，不适合对数据进行长期存储。

KVDB则是将数据存储在磁盘中，数据安全性级别高，不易丢失。



### global 变量

[Use of "global" keyword in Python - Stack Overflow](http://stackoverflow.com/questions/4693120/use-of-global-keyword-in-python)

[python - Using global variables in a function other than the one that created them - Stack Overflow](http://stackoverflow.com/questions/423379/using-global-variables-in-a-function-other-than-the-one-that-created-them)

---

[Global和Return - Python 进阶 - 极客学院Wiki](http://wiki.jikexueyuan.com/project/interpy-zh/global_return/README.html)

`global`变量意味着我们可以在函数以外的区域都能访问这个变量。

``` Python
# 首先，是没有使用global变量
def add(value1, value2):
    result = value1 + value2

add(2, 4)
print(result)

# Oh 糟了，我们遇到异常了。为什么会这样？
# python解释器报错说没有一个叫result的变量。
# 这是因为result变量只能在创建它的函数内部才允许访问，除非它是全局的(global)。
Traceback (most recent call last):
  File "", line 1, in
    result
NameError: name 'result' is not defined

# 现在我们运行相同的代码，不过是在将result变量设为global之后
def add(value1, value2):
    global result
    result = value1 + value2

add(2, 4)
print(result)
6
```

在实际的编程时，你应该试着避开`global`关键字，它只会让生活变得艰难，因为它引入了多余的变量到全局作用域了。

[python - Using global variables in a function other than the one that created them - Stack Overflow](http://stackoverflow.com/questions/423379/using-global-variables-in-a-function-other-than-the-one-that-created-them/423596#423596)

```Python
globvar = 0

def set_globvar_to_one():
    global globvar    # Needed to modify global copy of globvar
    globvar = 1

def print_globvar():
    print(globvar)     # No need for global declaration to read value of globvar

set_globvar_to_one()
print_globvar()       # Prints 1
```

只要在其中一个函数中声明 `global` ，在其他函数中就可以用了

关于全局变量的辩白：

> Globals are perfectly fine in every language that has ever existed and ever will exist. **They have their place.** What you should have said is they can cause issues if you have no clue how to program.

要根据规则来使用它们

> I think they are fairly dangerous. However **in python "global" variables are actually module-level**, which solves a lot of issues.

### 全局变量是邪恶的吗

[python - Why are global variables evil? - Stack Overflow](http://stackoverflow.com/questions/19158339/why-are-global-variables-evil/19158418#19158418)

### return

没有显式的return的话，Python默认return None

```python
return self.render.reply_text(from_user,toUser,int(time.time()),u"我是你大爷，"+content) 
# render方法是按 reply_text.xml 这个模板渲染，传入参数后就转换成微信要求的 XML 内容
```

## 装饰器

[Python装饰器学习 - thy专栏 - 博客频道 - CSDN.NET](http://blog.csdn.net/thy38/article/details/4471421)



## 指南

[python web 入坑指南 — python-web-guide 0.1 文档](http://python-web-guide.readthedocs.io/zh/latest/index.html)