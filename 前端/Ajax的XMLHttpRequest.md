# XMLHttpRequest属性



> onreadystatechange

指定当readState状态改变时的操作



> readystate

返回当前请求状态，只读



| 状态码 | 内容                                       |
| --- | ---------------------------------------- |
| 0   | 请求没有发出（调用open函数之前）                       |
| 1   | 请求已经建立，还没有发出（调用send函数之前）                 |
| 2   | 请求已经发出正在处理中（通常可以从响应头得到响应头部）              |
| 3   | 请求已经处理，正在接收服务器信息，响应中通常有部分数据可用，服务器还没有完成响应 |
| 4   | 响应已经完成，可以访问服务器响应并使用                      |

> responseBody

将回应信息正文以unsigned byte数组形式返回，只读



> responseStream

以Ado Stream对象形式返回响应信息，只读



> responseText

接收以普通文本返回的数据，只读



> responseXML

接收以XML文档形式回应的数据，只读



> status

返回当前请求的http状态码，只读



> statusText

返回当前请求的响应行状态，只读



> abort

取消当前所发请求



> getAllResponseHeader

取得所有的HTPP头信息



> getResponseHeader

取得一个指定的HTTP头信息





> **open**

open(String method,String url,boolean asynch,String username,String password)

method指post，get

url指地址

true异步，false同步

第四第五个是http认证



> **send**

将创建的请求发送到服务器端，接收回应信息

send(content)

get方式，不需要填写参数，或填null

post方式，把要提交的参数写上去



> **setRequestHeader**

setRequestHeader(String header,String value)

xmlhttp.setRequestHeader("C")

设置消息头(使用post方式使用，get方法不调用)

xmlhttp.setRequestHeader("Content-type","application/x-www-form-urlencoded")

设置一个指定请求的HTTP头信息



## 步骤

| 序号  | 内容                 |
| --- | ------------------ |
| 1   | 创建XMLHttpRequest对象 |
| 2   | 创建Http请求           |
| 3   | 设置响应Http请求状态变化的函数  |
| 4   | 设置获取服务器返回数据的语句     |
| 5   | 发送Http请求           |
| 6   | 局部更新               |


