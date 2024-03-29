# storage.js使用参考

---

Storage.js是一个基于HTML5 Web本地存储的扩展解决方案，虽然IE早期不支持本地存储(localStorage),但是可以通过userData来实现更多的本地数据存储。由于cookie本身的不可替代性，Storage.js也添加了对cookie的封装处理。

在介绍API之前，关于localStorage，userData，cookie有些特性需要说明一下：

- cookie会随着HTTP请求的头报文发送到服务端，而localStorage,userData则不会
- 三者可存储数据大小有区别
- localStorage本身没有失效时间，Storage.js对其添加了失效时间的扩展
- userData只能操作当前Path下的数据，为了方便不同Path下本地数据的共享，Storage.js通过htmlfile创建iframe指向到当前域根目录的favcion.icon下，实现同域不同Path数据共享与操作（所以必须保证根目录下favcion.icon存在）。

---


##使用范围

Storage.js是WEB端本地存储的解决方案，所以在做Web开发时，如果需要将数据存储到客户端，都可以使用Storage.js，当然一定要考虑两点：这些数据存储到客户端是否安全；本地可存储数据的大小。同时Storage.js还支持CommonJS和AMD标准规范，所以我们能够很方便的调用。

从0.3.1开始，Storage.js默认引用了json2.js:https://github.com/douglascrockford/JSON-js,这样可以方便的存储JSON,Array等Object数据。

## 使用说明

	在js文件中引用模块
	var storage = require('storage');

	storage.set(name,value,expires); //添加本地存储数据，有效期是expries(单位秒)
	storage.get(name); //获取本地存储数据
	storage.remove(name); //删除本地数据
	
	//以下是对cookie的处理
	
	storage.cookie.set(name,value,seconds,path,domain);
	storage.cookie.get(name);
	storage.cookie.remove(name);

		
##实例

	storage.set('store',{"type:"javascript","name":"Storage"},60) //存储{"type:"javascript","name":"Storage"}到store变量，有效期60s
	storage.get('store') //{"type:"javascript","name":"Storage"}
	storage.remove('store') //清空本地存储数据store