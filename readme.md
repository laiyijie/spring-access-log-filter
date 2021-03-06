# Spring accessLog filter

## Purpose


### Print the full accessLog

example：
	
	{"Q_URL":"http://bnm.xiaoxigua.me/server/api/v1/working/201707110338496382174971/points","_LOGGER_":"Access","Q_HEADERS":"{\"content-length\":\"201\",\"remoteip\":\"116.192.58.125\",\"cookie\":\"SESSION=ec8db250-0a95-4a80-b26d-d64aace787b4;\",\"host\":\"bnm.xiaoxigua.me\",\"content-type\":\"application/json; charset=UTF-8\",\"x-forwarded-for\":\"116.192.58.125\",\"accept-encoding\":\"gzip\",\"user-agent\":\"okhttp/3.6.0\"}","P_HEADERS":"{\"Connection\":[\"close\"],\"Content-Length\":[\"55\"],\"Date\":[\"Thu, 13 Jul 2017 08:23:20 GMT\"],\"Content-Type\":[\"application/json;charset=UTF-8\"]}","P_CODE":417,"_COST_":11,"Q_PARAM":"{}","Q_USERNAME":"26389","P_PAYLOAD":"{\"code\":800,\"message\":\"糟糕，服务器有点问题\"}","Q_METHOD":"POST","_TIME_":"2017-07-13 08:23:20.807 +0000","Q_PAYLOAD":"[{\"accuracy\":25.0,\"latitude\":31.262063,\"longitude\":121.483528,\"timestamp\":1499934195526,\"uid\":26392},{\"accuracy\":25.0,\"latitude\":31.262063,\"longitude\":121.483528,\"timestamp\":1499934200568,\"uid\":26392}]"}

在写给予SpringMVC的工程的时候，很多时候想要打印所有的请求日志（包括所有的request payload 和 response payload。而正常的使用过程中并无法把 response 和 request payload 都打印出来，因为HttpServletRequest中的outputstream以及HttpServletResponse中的body根本无从获取。


## Usage

1、 compile the project and import it into your project
	
	<groupId>me.laiyijie.util</groupId>
    <artifactId>spring-access-log</artifactId>
    <version>1.0.0</version>

2、 add filter in your web.xml 

	<filter>
        <filter-name>accessLogFilter</filter-name>
        <filter-class>cn.bangnongmang.server.log.web.AccessLogFilter</filter-class>
        <init-param>
            <param-name>usernameKey</param-name>
            <param-value>uid</param-value>
        </init-param>
    </filter>
    <filter-mapping>
        <filter-name>accessLogFilter</filter-name>
        <url-pattern>/*</url-pattern>
    </filter-mapping>

3、configure the System Environment Variable（the log path）

	B_LOGPATH=/your/log/path

you can change the log format by edit the log4j2.xml 
	

for more detail please check my blog

[http://laiyijie.me/2017/07/13/spring-accesslog-filter/](http://laiyijie.me/2017/07/13/spring-accesslog-filter/)