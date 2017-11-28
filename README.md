# cloudgo-datasql


#### 安装docker下载镜像以及启动mysql：<br>
这些部分按照老师上课给的博客做就行，在安装docker之前要更新自己的内核，使用<br>
sudo yum update即可。这里我要强调的是千万不要在更新内核过程中强制关机或者让<br>
系统处于待机状态（容易报错，然后不得不强制关机），否则会发现再也无法进入虚<br>
拟机,只能重新配置一个虚拟机并且重新配置所有的和go有关的东西。其它的操作没什么<br>
需要强调的。<br>

#### 创建数据库以及配置内容：<br>
这部分同样按照老师的博客做就可以，可以自行对用户表以及关联用户信息表内的数据<br>
进行修改。注意如果端口设置的不是3306的话，要在之后的程序中修改端口，否则无法<br>
正确运行程序。（老师的代码是默认3306）<br>

#### 测试web服务：<br>
使用 curl -d "username=ooo&departname=1"http://localhost:8080/service/userinfo <br>
命令传输数据到网站上。<br>
输入 curl http://localhost:8080/service/userinfo?userid= 查询上传的数据，结果如下：<br>
终端：<br>
![image](https://github.com/Tendernesszh/cloudgo-datasql/blob/master/running-result/cloudgo-data%E7%BB%88%E7%AB%AF.png)<br>
网页：<br>
![image](https://github.com/Tendernesszh/cloudgo-datasql/blob/master/running-result/cloudgo-data%E7%BD%91%E9%A1%B5.png)<br>

#### 使用xorm实现老师的程序之后的测试：<br>
和之前输入同样的测试命令，结果都是一样的。图片在测试结果的文件中，就不贴出来了。<br>

#### 压力测试：
在终端进入cloudgo-data文件夹，执行go run main.go 之后在命令行中输入<br>
ab -n 5000 -c 100 http://localhost:8080/service/userinfo 进行测试<br>
结果如下：<br>
![image](https://github.com/Tendernesszh/cloudgo-datasql/blob/master/running-result/cloudgo-data%E5%8E%8B%E5%8A%9B%E6%B5%8B%E8%AF%95.png)<br>
<br>
之后在终端中进入orm文件夹，执行go run main.go 之后在命令行中输入<br>
ab -n 5000 -c 100 http://localhost:8080/service/userinfo 进行测试<br>
结果如下：<br>
![image](https://github.com/Tendernesszh/cloudgo-datasql/blob/master/running-result/orm%E5%8E%8B%E5%8A%9B%E6%B5%8B%E8%AF%95.png)<br>
<br>
可以看出使用orm以后还是使得测试的完成稍微变慢了一点。<br>
不过我们使用orm是为了减少重复性代码，当我们实现一个应用程序时（不使用O/R Mapping），<br>
可能会写特别多数据访问层的代码，从数据库保存、删除、读取对象信息，而这些代码很多都是<br>
重复的。而使用orm即对象关系映射则会大大减少重复性代码，它主要实现程序对象到关系数据<br>
库数据的映射。<br>
使用orm的优点和缺点：<br>
优点：<br>
（1）提高开发效率，降低开发成本。<br>
（2）使开发更加对象化。<br>
（3）可移植。<br>
（4）可以很方便地引入数据缓存之类的附加功能。<br>
缺点：<br>
（1）自动化进行关系数据库的映射需要消耗系统性能。<br>
（2）在处理多表联查、where条件复杂之类的查询时，ORM的语法会变得复杂。<br>



