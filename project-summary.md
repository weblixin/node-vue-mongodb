# Project-Summary
项目总结

## 前端vue部分  

> ### 跨域问题
> + `main.js` 文件中 `Axios.defaults.withCredentials=true`
> + `ajax` 请求中加入： `withCredentials: false`

> ### 代理问题
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

> ### 路由问题
> + 路由中，children可以使页面在当前页面进行跳转
```javascript

    {
      path: '/home',
      component: Home,
      meta: {
        title: '系统首页'
      },
      children: [{
          path: '/adminlist',
          component: AdminList,
          meta: {
            title: '管理员列表'
          }
        },
        {
          path: '/message',
          component: Message,
          meta: {
            title: '客服消息'
          }
        }
      ]
    }

```

### 组件间的几种传值方式
> + 父传子 ===》
```javascript
      父组件：引入子组件 ---  :value1="value2" --- 引号中的 value2 需要在父组件的 data 中定义 --- value1 是子组件接收的字段;
      子组件：利用 props 接收 value1 字段，使用方式为 this.value1	
```
> + 子传父 ===》
```javascript
      父组件：引入子组件 ---  v-on:value1="value2" --- value1 需要在 methods 中定义 --- value2 是子组件传过来的字段;
      子组件：利用 $emit 进行传值，两个参数分别为父组件监听的事件 和 需要传的值，使用方式为 this.$emit('value2', value)
```
> + 非父子 ===》
```javascript
      同级目录下，创建一个bus.js文件，文件内容是暴露一个实例vue对象，在AB组件中引入bus.js
      A组件：this.$emit()
      B组件：this.$on()
```
> + 使用vuex ===》
```javascript
     使用vuex，将数据或方法保存在一个js文件中，然后暴露出去，在每个组件中引入该js文件
     state：store.state.datalist     mutations: store.commit('add', data)
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
