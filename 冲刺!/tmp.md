## View

* HTML templates
  * 绑定
  * 拾卡、报失
  * 登陆学校一卡通
    * 挂失
    * 查询流水
  * 手动查询

## Model

* 数据库设计
  * 用户信息
  * 失卡
  * 拾卡

## Control

* 模拟登陆

  * next-version：保存 cookies 类似

* 数据库操作

  * redis 缓存，后写入数据库
  * 数据写入和读取
    * 微信用户信息（openid、手机、卡号 等）
    * 拾卡（学号、地点……）
    * 失卡（学号……）

* 后台匹配查询

  * 相关逻辑

    * 有限状态（就是这个文件丢了）

  * 定时操作

    * > 英文叫 cron，微信自动回复有限制，可发手机

    * 无手机需要自己自动查询

* 用户手动查询结果

* 绑定用户

  * 手机
    * 短信验证
  * 微信用户信息
    * openid 等
  * 卡号

## 其他任务

* 本地搭建环境，跑一下校园微信公众号的那个项目

## 相关核心库

抛弃新浪云

### Flask

* Flask
  * 相关依赖(?)
    * Werkzeug：WSGI工具包，他可以作为一个Web框架的底层库
    * jinja2：模板引擎，作用就是把一个HTML 模板，以及一些环境变量，生成HTML 页面
      * MarkupSafe: 替换Jinja2 中附带的老的加速模块
* Flask-SQLAlchemy：操作数据库
  * 相关依赖(?)：MySQL-python、SQLAlchemy

## 其他

> todo

* celery：异步操作

* wechat-sdk
