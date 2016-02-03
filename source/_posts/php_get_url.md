### php 调用远程url的六种方法
1.用file_get_contents 以get方式获取内容

2.用fopen打开url, 以get方式获取内容

3.用file_get_contents函数,以post方式获取url

4.用fsockopen函数打开url，以get方式获取完整的数据，包括header和body

5.用fsockopen函数打开url，以POST方式获取完整的数据，包括header和body

6.使用curl库
