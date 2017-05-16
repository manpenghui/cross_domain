# cross-domain
node.js 的跨域解决方案
 ### 1.通过在node代码中加入以下代码：（express框架）
 ```
 app.all('*', function(req, res, next) {  
    res.header("Access-Control-Allow-Origin", "*");  
    res.header("Access-Control-Allow-Headers", "X-Requested-With");  
    res.header("Access-Control-Allow-Methods","PUT,POST,GET,DELETE,OPTIONS");  
    res.header("X-Powered-By",' 3.2.1')  
    res.header("Content-Type", "application/json;charset=utf-8");  
    next();  
});  
```
### 2.在chrome浏览器中通过以下方式解决

* 49之前的版本 在属性页面中的目标输入框里加上   --disable-web-security  如下图所示

![Alt text](/before49.jpg "before49 image")

点击应用和确定后关闭属性页面，并打开chrome浏览器。如果浏览器出现提示“你使用的是不受支持的命令标记 --disable-web-security”，那么说明配置成功。


* 49之后的版本

chrome的版本升到49之后，跨域设置比以前严格了，在打开命令上加--disable-web-security之后还需要给出新的用户个人信息的目录。众所周知chrome是需要用gmail地址登录的浏览器，登录后就会生成一个存储个人信息的目录，保存用户的收藏、历史记录等个人信息。49版本之后，如果设置chrome浏览器为支持跨域模式，需要指定出一个个人信息目录，而不能使用默认的目录，估计是chrome浏览器怕用户勿使用跨域模式泄露自己的个人信息（主要是cookie，很多网站的登录token信息都是保存在cookie里）。

具体做法为：

1)在电脑上新建一个目录，例如：C:\MyChromeDevUserData
 ![Alt text](/file.png "file image")

2)在属性页面中的目标输入框里加上   --disable-web-security --user-data-dir=C:\MyChromeDevUserData，其中--user-data-dir的值就是刚才新建的目录。
![Alt text](/after49.png "after49 image ")

3)点击应用和确定后关闭属性页面，并打开chrome浏览器。

再次打开chrome，发现有“--disable-web-security”相关的提示，说明chrome又能正常跨域工作了。
![Alt text](/chrome-expression.png "expression image ")
