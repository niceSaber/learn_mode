# Jquery
## 后退
通过js实现后退功能
1. ```windows.history.go(-1)```
2. ```windows.history.back()```
3. ```location.href = "后退指定页面的请求"```
## ajax
### ajax请求时，data所传的数据中的数组为空，请求报400
遇到这个问题时，请求会报**400**错误，因此可以在后台服务器端接收参数时
设置@RequestParam(value="数组的名称",required=false) 
required代表是否必传，默认为true，设为false后如果不传的话，默认赋值
为null




