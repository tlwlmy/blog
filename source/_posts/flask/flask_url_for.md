title: flask的url_for使用
date: 2016-06-15 16:59:42
tags:
---
### blueprint和url_for
	- 组织module的一个很好的方式, 通常我们会为不同的 Blueprint 设置不同的url prefix.	- 在设置了url prefix后, html 模板中与这个blueprint相关的link 字符串, 都需要加上url prefix, 否则路由地址就不对了.	- 当然这样的写法其实很是很糟糕的, hard code 的url prefix一多, 哪一天要调整这个url prefix就麻烦了
	- 最好的作法, 当然不是到处hard code 链接地址了, 推荐使用url_for()函数.  
	- 但加了url prefix之后, 使用 url_for() 函数时, 需要为view函数加一个命名空间, 到底这个命名空间取什么,  结论是 Blueprint的名称, 不是Blueprint对象的名称, 也不是python 模块的名称
### url_for使用例子
```python
#views.pyapp = Blueprint('user', __name__, url_prefix='/username')  #Blueprint的名称是 user@app.route("/user_info/<username>/<time_id>")def user_info(username, time_id):    return 'a,b,c,d,e'    def redirect_sample():    return redirect(url_for('user.user_info', user_name='tlwlmy', time_id='201406'))    模板上的写法也是一样,    <a href="{{ url_for('muser.user_info', report_name='tlwlmy', time_id='201406')}}">    get_user_info(201406)  </a>
```
### 参考文档
	- http://www.cnblogs.com/harrychinese/p/flask_tips.html
	- http://docs.jinkan.org/docs/flask/quickstart.html
