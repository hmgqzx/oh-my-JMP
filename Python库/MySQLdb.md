

## cursors 源码

[MySQLdb1/cursors.py at d34fac681487541e4be07e6978e0db233faf8252 · farcepest/MySQLdb1](https://github.com/farcepest/MySQLdb1/blob/d34fac681487541e4be07e6978e0db233faf8252/MySQLdb/cursors.py)

### execute 方法

从方法中可以看到用法，query 是 sql 语句（用 %s 表示占位），再传入对应参数，需要注意的是 query 中的%s 个数要和 args 元素个数（传入 list、tuple 等）一样

相关：

[MySQL :: MySQL Connector/Python Developer Guide :: 10.5.4 MySQLCursor.execute() Method](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysqlcursor-execute.html)

参数个数不确定，需要自动生成对应 %s 个数，参考：

[MySQLdb 参数处理的坑 - Xupeng's blog](https://blog.xupeng.me/2013/09/25/mysqldb-args-processing/)

```Python
    def execute(self, query, args=None):

        """Execute a query.
        
        query -- string, query to execute on server
        args -- optional sequence or mapping, parameters to use with query.
        Note: If args is a sequence, then %s must be used as the
        parameter placeholder in the query. If a mapping is used,
        %(key)s must be used as the placeholder.
        Returns long integer rows affected, if any
        """
        del self.messages[:]
        db = self._get_db()
        if isinstance(query, unicode):
            query = query.encode(db.unicode_literal.charset)
        if args is not None:
            if isinstance(args, dict):
                query = query % dict((key, db.literal(item))
                                     for key, item in args.iteritems())
            else:
                query = query % tuple([db.literal(item) for item in args])
        try:
            r = None
            r = self._query(query)
        except TypeError, m:
            if m.args[0] in ("not enough arguments for format string",
                             "not all arguments converted"):
                self.messages.append((ProgrammingError, m.args[0]))
                self.errorhandler(self, ProgrammingError, m.args[0])
            else:
                self.messages.append((TypeError, m))
                self.errorhandler(self, TypeError, m)
        except (SystemExit, KeyboardInterrupt):
            raise
        except:
            exc, value, tb = sys.exc_info()
            del tb
            self.messages.append((exc, value))
            self.errorhandler(self, exc, value)
        self._executed = query
        if not self._defer_warnings: self._warning_check()
        return r
```

