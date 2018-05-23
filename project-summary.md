# Project-Summary
项目总结

## 前端vue部分  

> ### 跨域问题
> + `main.js` 文件中 `Axios.defaults.withCredentials=true`
> + `ajax` 请求中加入： `withCredentials: false`

> ### 代码问题

> + 使用代理，将vue项目放到后台项目中---在config/index中添加代理

```javascript

    proxyTable: {// 代理表
  	// key ： value
  	// 代理的路劲 ： 代理的规则
    	'/VueHandler':{
    		target:"http://localhost:3000",// 目标服务器 node后台
    		changeOrigin:true,// 改变服务器的 源
    									//请求的路径           改变后的路径
    		pathRewrite:{'/VueHandler':'/VueHandler'}// 重写的规则
    	},
        '/DownLoadPicHandler':{
            target:"http://localhost:3000",// 目标服务器 node后台
            changeOrigin:true,// 改变服务器的 源
                                        //请求的路径           改变后的路径
            pathRewrite:{'/DownLoadPicHandler':'/DownLoadPicHandler'}// 重写的规则
        }

    },

```

## 后台node部分

> ### 跨域问题
> + `app.js` 文件中加入 

```javascript  

app.all('*', function(req, res, next) {
	var oriRefer;
	if(req.headers.referer){
	oriRefer= req.headers.referer.substring(0,req.headers.referer.indexOf("/",10));
	}
	res.header("Access-Control-Allow-Origin", oriRefer?oriRefer:"*");
	res.header('Access-Control-Allow-Credentials', true);
	res.header("Access-Control-Allow-Headers", "Origin, X-Requested-With, Content-Type, Accept");
	res.header("Access-Control-Allow-Methods","PUT,POST,GET,DELETE,OPTIONS");
	res.header("X-Powered-By",' 3.2.1')
	next();
});

```

## 数据库mongodb部分
