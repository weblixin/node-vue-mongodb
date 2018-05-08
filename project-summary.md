# Project-Summary
项目总结

## 前端vue部分  

### 跨域问题

+ `main.js` 文件中 `Axios.defaults.withCredentials=true`
+ `ajax` 请求中加入： `withCredentials: false`

## 后台node部分

+ `app.js` 文件中加入 

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
