# 常用模块
- calendar
- time
- datetime
- timeit
- os
- shutil
- zip
- math
- string
- 上述所有模块使用理论上都应该先导入，string是特例



# calendar
- 使用前先导入 import calendar
- calendar：获取一年的日历字符集
- isleap：判断某一年是否是闰年
- leapdays：获取指定年份之间的闰年的天数
- month：获取某个月的日历字符串
- monthrange：获取一个月从周几开始和此个月的天数
- monthcalendar：返回一个月每天的矩阵列表
- prcal：直接打印日历
- prmonth：直接打印某个月的日历
- weekday：获取周几

# time
- 时间戳
    - 一个时间表示，根据不同语言，可以是整数挥着浮点数
    - 是从1970年1月1日0时0分0秒到现在经历的秒数
    - 如果表示的时间是1970年以前或者太遥远的未来，可能出现异常
    - 32位操作系统能够支持到2038年
- UTC时间
    - UTC又称为世界协调时间，以英国的格林尼治天文所所在地区的时间作为参考的时间，也叫做世界标准时间
    - 中国时间是UTC+8东八区
- 夏令时
    - 夏令时就是在夏天的时候将时间调快一小时，本意是督促大家早睡早起节省蜡烛，每天变成25小时，本质没变还是24个小时
- 时间元组
    - 一个包含时间内容的普通元组
    
- 使用需要导入 import time
- 时间模块的属性
    - timezone：当前时区和UTC时间相差的秒数，在没有夏令时的情况下的间隔
    - altzone：获取当前时区与UTC时间相差的秒数，在有夏令时的情况下
    - daylight：测当前是否是夏令时时间状态，0表示是
- time：获取时间戳
- localtime：得到当前时间的时间结构
- asctime：返回元组的正常字符串化之后的时间格式
- ctime：获取字符串化的当前时间
- mktime:使用时间元组获取对应的时间戳
- clock：获取cpu时间（即一段代码执行时间），版本3.6调用有问题
- sleep：使程序进入睡眠，n秒后继续
- strftime：将时间元组转化为自定义的字符串格式

# datetime
- datetime提供日期和时间的运算和表示
- 使用需要先导入 import datetime
- datetime的属性
    - date：提供一个理想和的日期
    - time：提供一个理想和的时间
    - datetime：提供日期和时间的组合
    - timedalte：提供一个时间差，时间长度
- today：
- now：
- utcnow：
- fromtimestamp：从时间戳中返回本地时间

# timeit - 时间测量工具

# os - 操作系统相关
- 跟操作系统相关，主要是文件操作
- 与系统相关的操作，主要包含在三个模块里
    - os：操作系统目录相关
    - os.path：系统路径相关操作
    - shutil：高级文件操作，目录树的操作，文件复制，删除，移动
    
#os
- getcwd：获取当前的工作目录
- chdir：改变当前的工作目录
- listdir：获取一个目录中所有子目录和文件的名称列表
- makedirs：地柜创建文件夹
- system：运行系统shell命令
- getenv：获取指定的系统环境变量值
- putenv：设置环境变量值
- exit：退出当前程序
- 属性
    - os.curdir：当前目录
    - os.pardir：父目录
    - os.sep：当前系统的路径分隔符
    - os.linesep：当前系统的换行符号
    - os.name：当前系统名称
    
#os.path模块，跟路径相关的模块
- abspath：将路径转换为绝对路径
- basename：获取路径中的文件名部分
- join：将多个路径拼合成一个路径
- split：将路径切割为文件夹部分和当前文件部分
- isdir：检测是否是目录
- exists：检测文件或者目录是否存在

#shutil模块
- copy：复制文件（拷贝的同时可以给文件重命名）
- copy2：复制文件，保留元数据
- copyfile：将一个文件中的内容复制到另一个文件当中
- move：移动文件/文件夹
- make_archive：归档操作
- unpack_archive：解包操作

#zipfile模块
- ZipFile：创建一个ZipFile对象，表示一个zip文件，参数file表示文件的路径或类文件对象
- getinfo：获取zip文档内指定文件的信息，返回一个zipfile.ZipInfo对象，它包括文件的详细信息
- namelist：获取zip文档内所有文件的名称列表
- extractall：解压zip文档中的所有文件到当前目录

#random模块
- 所有的随机模块都是伪随机
- random：获取0-1之间的随机小数
- choice：随机返回序列中的某个值
- shuffle：随机打乱列表
- randint：随机获取一个区间的整数