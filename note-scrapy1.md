# 爬虫简介
- python网络包
    - python2.x：urllib，urllib2，urllib3，httplib，httplib2，requests
    - python3.x：urllib，urllib3，httplib2，requests
    - python2：urllib和urllib2配合使用，或者requests
    - python3：urllib，requests
    
    
# urllib
- 包含模块
    - urllib.request：打开和读取urls
    - urllib.error：包含urllib.request产生的常见的错误，使用try捕捉
    - urllib.parse：包含解析url的方法
    - urllib.robotparse：解析robots.txt文件
    
- 网页编码问题的解决
    - chardet：可以自动检测网页的编码格式,但是可能有误
    - 需要安装 conda install chardet
    
- urlopen的返回对象
    - geturl：返回请求对象的url
    - info：请求反馈对象的meta信息
    - getcode：返回的http code
    
- request.data的使用
    - 访问网络的两种方式
        - get
            - 利用参数给服务器传递信息
            - 参数为dict，然后用parse编码
        - post
            - 一般向服务器传递参数使用
            - post是把信息自动加密处理
            - 我们如果想使用post信息，粗腰使用data参数
            - 使用post，意味着Http的请求头可能需要更改：
                - Content-Type:application/x-www.form-urlencode
                - Content-Length:数据长度
                - 简而言之，一旦更改请求方法，请注意其他请求头部信息相适应
             - urllib.parse.urlencode可以将字符串自动转换成上面的
             - 为了更多的设置请求信息，单纯的通过urlopen函数已经不太好用了
             - 需要使用request.Request类
             
             
             
- urllib.error
    - URLError产生的原因：
        - 没网
        - 服务器连接失败
        - 不知道指定服务器
    - 是OSError的子类
    - HTTPError,是URLError的一个子类
    - 两者区别：
        - HTTPError是对应的HTTP请求的返回码错误，如果返回错误码是400以上，则引发HTTPError
        - URLError对应的一般是网络出现问题，包括url问题
       
       
- UserAgent
    - userAgent：用户代理，简称UA，属于headers的一部分，服务器通过UA来判断访问者身份
    - 常见的UA值，使用的时候可以直接复制粘贴，也可以用浏览器访问的时候抓包
    - 设置UA可以通过两种方式：
        - headers
        - add_header
        
- ProxyHandler处理（代理服务器）
    - 使用代理IP是爬虫的常用手段
    - 获取代理服务器的地址：
        - www.xicidaili.com
        - www.goubanjia.com
    - 代理用来为隐藏真是访问中的ip，代理也不允许频繁访问某一个固定网站，所以，代理一定要很多很多
    - 基本使用步骤：
        - 1. 设置代理地址
        - 2. 创建ProxyHandler
        - 3. 创建Opener
        - 4. 安装Opener
        
- cookie & session
    - 由于http协议的无记忆性，人们为了弥补这个缺憾， 所采用的一个补充协议
    - cookie是发放给用户（即http浏览器）的一段信息，session是保存在服务器上的对应的另一半信息，用来记录用户信息
    
- cookie和session的区别
    - 存放位置不同
    - cookie不安全
    - session会保存在服务器上一定时间，会过期
    - 单个cookie保存数据不超过4k，很多浏览器限制一个站点最多保存20个cookie
- session的存放位置
    - 存在服务器端
    - 一般情况，session是放在内存中或者数据库中
- cookie
    - 可以看到，没使用cookie则反馈网页为未登录状态
    - 而通过浏览器F12查看数据包后可以知道登录后的cookie，直接把cookie复制下来，然后手动放入请求头，就可以得到已登录的网页
    - http模块包含一些关于cookie的模块，通过这些模块我们可以自动使用cookie
        - CookieJar 
            - 管理存储cookie，向传出的http请求添加cookie
            - cookie存储在内存中，CookieJar实例回收后cookie将消失
        - FileCookieJar(filename, delayload=None, policy=None)
            - 使用文件管理cookie
            - filename是保存cookie的文件
        - MozillaCookieJar(filename, delayload=None, policy=None)
            - 创建与mozilla浏览器cookie.txt兼容的FileCookiejar实例
        - LwpCookiejar(filename, delayload=None, policy=None)
            - 创建与libwww-perl标准兼容的Set-Cookie3格式的FileCookieJar实例
        - 他们的关系是：CookieJar-->FileCookieJar-->MOzillaCookieJar & LwpCookieJar
        - 利用CookieJar访问人人网，案例cookiejartest.py
            - 自动使用cookie登录，大致流程：
                - 打开登录页面后自动通过用户名和密码登录
                - 自动提取反馈回来的cookie
                - 利用提取的cookie登录隐私机页面
        - handler是Handler的实例
            - 用来处理复杂的请求
        - 创立handler后，使用openner打开，打开后相应的业务由相应的handler处理，比如请求头有什么代理服务器，用户代理，还有一些https的东西之类的，就由各自的处理器自己处理
        - cookie作为一个变量，可以打印出来
            - cookie的属性
                - name：名称
                - value：值
                - domain：可以访问此cookie的域名
                - path：可以访问此cookie的页面路径
                - expire：过期时间
                - size：大小
                - Http字段
        - cookie的保存，案例savecookie.py
        - cookie的读取，案例readcookie.py
    - SSl
        - SSL整数就是指遵守SSL安全套阶层协议的服务器数字证书（SercureSocketLayer）
        - 美国网景公司开发
        - CA（CertifacateAuthority）是数字证书认证中心，发放，管理，废除数字证书的授信人的第三方机构，即他来证明你要访问的该网站是安全可靠的
        - 遇到不信任的SSL证书，需要单独处理，案例ssltest
    - js加密
        - 有的反爬虫策略采用js对需要传输的数据进行加密处理（通常是取md5值）
        - 经过加密，传输的就是密文，但是加密函数或者过程一定是在浏览器完成，也就是一定会把代码（js代码）暴露给使用者
        - 通过阅读加密算法，就可以模拟出加密过程，从而达到破解
        - 案例jiamijs.py
    - ajax
        - 异步请求
        - 一定会有url，请求方法，可能有数据
        - 一般使用json格式
        - 案例ajaxtest.py(用的豆瓣电影网站，浏览某个类型的电影时，滚动滑动条到底部又会加载一部分，这就是用的ajax)
        
#Requests - 献给人类
- Http for Humans更简洁更友好
- 继承了urllib的所有特征
- 底层使用的是urllib3
- 开源地址：https://github.com/requests/requests
- 中文文档：http://docs.python-requests.org/zh_CN/latest/index.html
- 因为是第三方库，所以需要安装conda install requests
- get请求
    - requests.get(url)
    - requests.request("get", url)
    - 可以带有headers和param参数
    - 案例requestsgettest.py
- get的返回内容
    - 案例returngettest.py
- post
    - rsp = requests.post(url, data=data)
    - 案例requestsposttest.py
    - data,headers要求是dict类型，不需要编码
- proxy
    - 
    proxies = {
    "http":"addrs of proxy",
    "https":"addrs of proxy",
    }
    rsp = requests.request("get",url,proxies=proxies)
    - 代理有可能会报错，如果使用人数多，考虑安全问题，可能会被强行关闭
    
- 用户验证
    - 代理验证（私密代理）
    - 可能需要使用HTTP basic Auth，可以这样
    #格式为 用户名：密码@代理地址：端口地址
    proxy = {"http": "china:123456@192.168.1.1:1111"}
    rsp = requestd.get(url, proxies=proxies)
- web客户端验证
    - 如果遇到web客户端验证，需要添加auth=（用户名，密码）
    auth=("test1", "123455")#授权信息
    rsp=requests.get(url, auth=auth)
- cookie
    - requests可以自动处理cookie信息
    rsp=requests.get(url)
    #如果对方服务器给你传送了cookie信息，则可以通过反馈的cookie属性得到
    会返回一个cookiejar实例
    cookiejar= rsp.cookie
    #可以将cookiejar转换成字典
    cookiedict=request.utils.dict_from_cookiejar(cookiejar)
    
- session
    - 跟服务器端session不是一个东西
    - 模拟一次对话，从客户端浏览器链接服务器开始，到客户端浏览器断开
    - 能让我们跨请求时保持某些参数，比如在同一个session实例发出的所有请求之间保持cookie
    - #创建session对象，可以保存cookie值
    ss = requests.session()
    headers = {"User-Agent":"xxxxxx"}
    data = {"name"："xxxxxxx"}
    #此时，由创建的session管理请求，负责发出请求
    ss.post(url,data=data,headres=headers)
- https请求验证ssl证书
    - 参数verify负责表示是否需要验证ssl证书，默认是True
    - 如果不需要验证ssl证书，则设置成False表示关闭
     rsp = requests.get(url, verify=False)
     #如果用verify=True访问12306会报错，因为证书有问题
    