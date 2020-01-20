[![Run on Repl.it](https://repl.it/badge/github/zhang0peter/bilibili-user-information-spider)](https://repl.it/github/zhang0peter/bilibili-user-information-spider)

## 声明

* 代码、教程均为本人原创，且仅限于学习交流，请勿用于任何商业用途！   

********
2020-1-20 更新：增加log模块，修复代码bug

之前写了B站视频信息的爬虫，然后就想到了爬取B站的用户信息。                
在2018年3月11号，B站的第3亿用户诞生了。                

## 准备工作
我使用的是Python3，数据库用的是Python自带的sqlite，使用requests库爬取。              
安装需要的库              

```python
pip install requests
```

本来我的打算是通过post来获取用户信息的，但发现这样做很容易被封。                
在考虑良久后，我觉得通过用户的手机端页面来获取用户信息，这样不容易被封。                
比如在手机上访问https://m.bilibili.com/space/2
这个页面，可以获取用户名，性别，等级的信息。                
然后再通过api接口来获取用户的关注和粉丝数，如https://api.bilibili.com/x/relation/stat?jsonp=jsonp&vmid=2                
```javascript
{
  "code":0,
  "data":{
          "mid":0,
          "following":116,
          "whisper":0,
          "black":0,
          "follower":327153},
  "message":"0",
  "ttl":1}
```
使用requests库获取数据，可以使用多线程爬虫进行加速，多线程的代码我不放出来。               


## 数据获取
B站对爬虫采取的是一旦发现，就封ip一天到5天不等。              
可以使用代理防封IP。               
在累计爬到一亿多时，我发现ip被封的很频繁，于是就不再爬下去了，因为这3亿用户有太多的僵尸用户了。                
比如:                
![](information.png)                
从图上可以看出这一面的用户基本都是僵尸用户，除了少数几个有等级或者关注的。                
应该是16年B站开放注册后僵尸用户一下子就多起来了。                
我就不把自己爬到的全部数据放上来了,就前**109万**用户的数据放上来，在data.db里。                






爬虫代码见 [bilibili-user-information-spider.py](spider.py)              
参考资料： [bili-user](https://github.com/airingursb/bilibili-user/)              
