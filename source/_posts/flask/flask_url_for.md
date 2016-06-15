title: flask的url_for使用
date: 2016-06-15 16:59:42
tags:
---
### blueprint和url_for
	- 组织module的一个很好的方式, 通常我们会为不同的 Blueprint 设置不同的url prefix.
	- 最好的作法, 当然不是到处hard code 链接地址了, 推荐使用url_for()函数.  
	- 但加了url prefix之后, 使用 url_for() 函数时, 需要为view函数加一个命名空间, 到底这个命名空间取什么,  结论是 Blueprint的名称, 不是Blueprint对象的名称, 也不是python 模块的名称
### url_for使用例子
```python
#views.py
```
### 参考文档
	- http://www.cnblogs.com/harrychinese/p/flask_tips.html
	- http://docs.jinkan.org/docs/flask/quickstart.html