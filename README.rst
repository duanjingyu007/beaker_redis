一、当前使用说明:

python setup.py install


或者

1. python setup.py sdist
2. sudo pip install dist/beaker_redis-1.0.2.tar.gz

第1句打包源码
第2句使用pip安装

二、配置

对pyramid的项目ini文件类似如下配置：

```
; For pyramid_beaker
;session.type = mongodb
;session.url = mongodb://192.168.1.245:27017/beaker.sessions

session.type = redis
;session.url = ss3796@192.168.1.245:5379/1
session.url = sentinel:ss3796@192.168.1.245:25379/session79/1
session.hkey_prefix =
session.key =JSESSIONID
session.block_custom_class = true
```

***注意：***

1. 可以实现共享，但是判断登录条件之类，需要采用共同的字段才能保证
2. 自定义class对象有些问题，java的自定义对象python无法识别，但是python不会破坏，可以继续使用。python的自定义对象会被java破坏，所以别用
3. 要避免同样的session key存储不一样的东西，那样会互相破坏
4. Java的自定义对象需要实现Serializable接口才可以设置到session，否则异常


