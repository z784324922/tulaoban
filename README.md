# tulaoban

###2017.12.25
1.返回站点根路径
	request.getContextPath()
2.返回请求用的计划名,如:http.https及ftp等
	request.getScheme()
3.返回接受请求的服务器主机名
	request.getServerName()

###2017.12.26
1.c:forEach
	<c:forEach var="每个变量名字"   items="要迭代的list"   
		varStatus="每个对象的状态"  begin="循环从哪儿开始"    
		end="循环到哪儿结束"    step="循环的步长">
		循环要输出的东西
	</c:forEach>
2.directive 告诉容器如何处理JSP处理的请求和响应
	<%@ directive attribute = "value" %>
3.@符号和指令名称之间，以及最后一个属性和关闭％>之间的空格是可选的
4.JSP中有三种类型的指令标签:
(1)page指令用于向容器提供与当前JSP页面相关的指令
	<%@ page attribute = "value" %>
(2)include指令用于在编译阶段包括一个文件
	<%@ include file = "relative url" >
(3)声明了一个标签库，包含自定义动作，用在页面中
	<%@ taglib uri="uri" prefix = "prefixOfTag" >

###2017.12.27
1.<c:choose>, <c:when>, <c:otherwise>标签,类似switch
**test评估条件,必须有 ,默认none
	<c:choose>
		<c:when test="${salary <= 0}">
			Salary is very low to survive.
		</c:when>
		<c:when test="${salary > 5000}">
			Salary is very good.
		</c:when>
		<c:otherwise>
			No comment sir...
		</c:otherwise>
	</c:choose>

###2017.12.27
**antd组件使用报错，先检查版本号与官方文档是否一致

###2018.1.11
1.使用uploadfy时，必须打开flash，不然会报错
2.uploadify 上传出现 security error错误:
	//新建xml文本,并命名为crossdomain.xml,添加内容
	<?xml version="1.0" encoding="UTF-8"?>
	<!DOCTYPE cross-domain-policy SYSTEM 
			"http://www.macromedia.com/xml/dtds/cross-domain-policy.dtd" >
	<cross-domain-policy>
		<site-control permitted-cross-domain-policies="all" />
		<allow-access-from domain="*" /> //此处"*"换成 "*.网站域名"
		<allow-http-request-headers-from domain="*" headers="*" />
	</cross-domain-policy>
	//把文件保存并上传到网站的根目录

###2018.1.12
1.二次加载百度地图,需要延迟处理:
	setTimeout(function(){init();},200);
2.使用bootstrap后,百度地图label显示会出问题
	原因: bootstrap给label默认了一个max-width：100%

###2018.1.16
qs是npm仓库锁管理的包，可通过npm i qs命令进行安装
1.qs.parse()将URL解析成对象的形式
	const Qs = require('qs');
	let url = 'method=query_sql_dataset_data&projectId=85&appToken=7d22e38e-5717-11e7-907b-a6006ad3dba0';
	Qs.parse(url);
	console.log(Qs.parse(url));
2.qs.stringify()将对象解析成URL的形式
	const Qs = require('qs');
	let obj= {
	     method: "query_sql_dataset_data",
	     projectId: "85",
	     appToken: "7d22e38e-5717-11e7-907b-a6006ad3dba0",
	     datasetId: " 12564701"
	   };
	Qs.stringify(obj);
	console.log(Qs.stringify(obj));

###2018.1.25
使用es6语法Object.assign导致的ie兼容问题
1.全局引入babel-polyfill
	import 'babel-polyfill'
2.使用babel-plugin-transform-runtime
	{
	  "plugins": [
	    ["transform-runtime", {
	      "helpers": false, 
	      "polyfill": true, 
	      "regenerator": true, 
	      "moduleName": "babel-runtime"
	    }]
	  ]
	}

###2018.1.28
axios上传图片问题
    const instance=axios.create({
        withCredentials: true
    })
    instance.post("http://test.tulaoban.net/earthworkweb/base/upload",
        formdata
    )

###2018.2.6
webpack打包文件过大
1.注释:
	fiol:"source-map"
2.添加：
	plugins:[
        new UglifyJSPlugin()
    ]

###2018.3.3
1.Date.parse()获取时间戳IOS不兼容的问题(IOS为NaN的问题)
IOS只识别2017/01/01这样的日期格式，不识别2017-01-01
	var data = '2017-01-01 11:00:00';  
	mydata=data.replace(/-/g, '/');  
	console.log("返回时间：" + mydata);  
	var time = Date.parse(new Date(mydata)) / 1000; 

###2018.3.19
1.wepy创建新的page,每次创建需要保存才能正常运行,命名不要大写

###2018.3.20
1.微信小程序e.target和e.currentTarget区别
e.target:就是你点击的元素(不一定是你绑定事件的元素)
e.currentTarget:绑定事件的元素
2.微信小程序cover-view暂不支持box-shadow等css属性
3.微信小程序页面的json文件里面添加  "disableScroll": true;true:禁止弹动，false：为默认允许弹动

###2018.3.27
微信授权登录，先进去一个中间页再window.location.href到微信授权页，不然会一边渲染当前页面一遍跳转授权页

###2018.4.2
1.wepy在异步函数中更新数据的时，必须手动调用$apply方法，才会触发脏数据检查流程的运行,如:
	setTimeout(() => {
	    this.title = 'this is title';
	    this.$apply();
	}, 3000);
2.线上小程序的接口请求必须是https
3.await只能在async函数中运行

##2018.4.15
windows环境下创建react-native项目:
1.安装node
	npm install -g yarn react-native-cli
2.安装jdk1.8版本(通过java -version检测)
3.安装android sdk
4.配置环境变量
5.创建RN项目
	react-native init Project
6.运行package
	cd Project
	react-native start
访问:http://localhost:8081/index.android.bundle?platform=android
7.检查设备
	adb devices
8.运行项目
	react-native run-android
9.在设备上运行
(1)android 5.0及以上使用USB连接电脑
	adb reverse tcp:8081 tcp:8081
	摇一摇  使用Reload JS
(2)android 5.0以下通过wifi连接电脑
	首先确保你的电脑和手机设备在同一个Wi-Fi环境下。
	在设备上运行你的React Native应用。和打开其它App一样操作。
	你应该会看到一个“红屏”错误提示。这是正常的，下面的步骤会解决这个报错。
	摇晃设备，或者运行adb shell input keyevent 82，可以打开开发者菜单。
	点击进入Dev Settings。
	点击Debug server host for device。
	输入你电脑的IP地址和端口号（譬如10.0.1.1:8081）。
		在Mac上，你可以在系统设置/网络里找查询你的IP地址。
		在Windows上，打开命令提示符并输入ipconfig来查询你的IP地址。
		在Linux上你可以在终端中输入ifconfig来查询你的IP地址。
	回到开发者菜单然后选择Reload JS。
