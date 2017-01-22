[web.py 0.3 新手指南 (web.py)](http://webpy.org/docs/0.3/tutorial.zh-cn)

**导入**

```Python
import web
```

**将URL结构告诉web.py**

```Python
urls = (
'/weixin','WeixinInterface'
)
```

第一部分是匹配URL的正则表达式，第二部分是接受请求的类名称

**创建一个列举这些url的application**

```Python
app = web.application(urls, globals())

app = web.application(urls, globals()).wsgifunc() # wsgifunc()是新浪云的函数
```

## Render

**class** ` Render(self, loc='templates', cache=None, base=None, **keywords)`

The most preferred way of using templates.

```Python
render = web.template.render('templates')
print render.foo()
```

Optional parameter can be `base` can be used to pass output of every template through the base template.

```Python
render = web.template.render('templates', base='layout')
```

## 数据库操作

**注意:** 在你开始使用数据库之前，确保你已经安装了合适的数据库访问库。比如对于MySQL数据库，使用 [MySQLdb](http://sourceforge.net/project/showfiles.php?group_id=22307) 

