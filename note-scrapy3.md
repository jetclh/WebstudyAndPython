# 动态html分解
- JavaScript
- JQuery
- Ajax
- DHTML
- python采集动态数据
    - 从javascript代码入手采集
    - python第三方运行javascript，直接采集你在浏览器看到的页面
    
    
# Selenium + PhantomJS
- selenium：web自动化测试工具
    - 自动加载页面
    - 获取数据
    - 截屏
    - 安装：pip install selenium==2.48.0
    - 官网：收藏夹
    
- PhantomJS
    - 基于webkit的无界面的浏览器
    - 官网：收藏夹
    - 直接去网上下载即可，代码中直接用webdriver来调用浏览器，如果找不到浏览器，需要指定浏览器的位置
- Selenium 库有一个WebDriver的API
- WebDriver可以跟页面上的元素各种交互，用它可以来进行爬取
- 案例seleniumtest.py

# chrome + chromedriver
- 下载安装Chrome
- 下载安装chromedriver
- selenium操作主要分为两大类：
    - 得到UI元素
        - find_element_by_id
        - find_elements_by_name
        - find_elements_by_xpath
        - find_elements_by_link_text
        - find_elements_by_partial_link_text
        - find_elements_by_tag_name
        - find_elements_by_class_name
        - find_elements_by_css_selector
    - 基于UI元素操作的模拟
        - 单击
        - 右键
        - 拖拽
        - 输入
        - 可以通过导入ActionChains类来做到
    - 案例chrometest.py
    
    
    
# 验证码问题
- 验证码：判断是否是机器人或者爬虫
- 分类：
    - 简单图片
    - 极验，官网：www.geetest.com
    - 12306
    - 电话
    - google验证
- 验证码破解;
    - 通用方法：
        - 下载网页和验证码
        - 手动输入验证码
    - 简单图片：
        - 使用图像识别软件或者文字识别软件
        - 可以使用第三方图像验证码破解网站，www.chaojiying.com
    - 极验：
        - 可以模拟鼠标等移动
    - 12306：
        - 手动识别
    - 电话：
        - 语音识别
        
# Tesseract
- 机器视觉领域的基础软件
- OCR：OpticalCharacterRecognition，光学文字识别
- Tessert：一个ocr库，由google赞助
- 安装：
    - windows：百度搜索
    - Mac：brew install tesseract
    - Linux：apt-get install tesseract-ocr
    - 安装完成后需要设置环境变量
- 安装完成后还需要pytesseract
    - pip install pytesseract
     

