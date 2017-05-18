###已知一个数组，数组内任意两个元素求差，求差的最大值，并输出。

```
	var a = [1,3,5,7,20];
    function findMaxDifference(arr, len) {
        var arrMax = Math.max.apply(null, arr);
        var arrMin = Math.min.apply(null, arr);
        Promise.resolve().then(function(){
            var nMax = arrMax - arrMin;
            return nMax;
        }).then(function(nMax){
            console.log('nMax = ' + nMax);
        });
    }

    findMaxDifference(a, a.length)

```

考察点：

* [] 没有求最大值最小值函数, 可以借助Math函数方法
* apply 方法使用


###将数组[1,[1,2,[1,2,3]]] 扁平化为[1,1,2,1,2,3];
```
let arr = [1,[1,2,[1,2,3]]];
arr.join(',').split(',')
```

```
var aNew = [];
	function  flatten(arr){
		for(var key in arr){
			if(arr[key] instanceof Array){
				arguments.callee(arr[key]);
			}else{
				aNew.push(arr[key]);
			}
		}
		return aNew;
	}
	var a = [1,2,3,[4,5,6,[7,8,9,10,[11]],12],13];
	var b =  flatten(a);
```
考察点：

* join 方法使用
* arguments.callee、instanceof使用

###判断true or false

```
	(function(){}) == false false
    null == undefined  true
    null == false false
    undefined == false false
```
    
###随机生成一个长度为10的数组，之后降序排列
```
var arr = [];
		flag = true;
	while(flag){
		if(arr.length < 10){
			arr.push(Math.floor(Math.random() * 100 + 10));
		}else{
			flag = false;
		}
	}
	var result = arr.sort(function(a, b){
		return a>=b ? -1 : 1;
	});
	console.log(result);
	```
考察点：
* sort 使用，回调返回非负数，不动，返回负数，调换位置
* 实现sort
	
	
###写出位置1，2的输出结果
```
var vv = 'window.vv'
var ob = {
    vv: 'ob-vv',
    b: function (){
        console.log(this.vv)
    }
}
ob.b(); //1

var obb = ob.b;
obb();  //2

```
答案：ob-vv window.vv 
考察点：
* 闭包
* this作用域

###了解co吗？实现generator执行器。
```
function co(genFunc) {
    var gen = genFunc();
    return function(fn) {
        next();
        function next(res, err) {
            if (err) return fn(err);
            var ret = gen.next(res);
            if (!ret.done) return ret.value.then(next);
            fn && fn(null, err);
        }
    };
}
co(function*() {
    var a = yield f_a();
    var b = yield f_b(a);
    var c = yield f_c(b);
    console.log(a,b,c)
})();
function f_a() {
    return new Promise(function(resolve, reject) {
        setTimeout(function () {
            console.log('5 s')
            resolve(1)
        } ,5000)
    })
}
function f_b(a) {
    return Promise.resolve(a + 3);
}
function f_c(b) {
    return Promise.resolve(b + 6);
}
```
考察点：

* 知识面及对es6 的了解
* 是否真正理解generator

###是否了解Promise，尝试实现Promise



###向对象中push 东西，输出结果

```
var oBj = {'1':'a','2':'b','length':2,push:Array.prototype.push}
	oBj.push('c'); //长度变为3，oBj[2]变成c，oBj[3]是undefined
	console.log(oBj, oBj[0], oBj[1], oBj[2], oBj[3]);
```
考察点：

* push 方法使用
* 对象的数组式使用

###解析url ？后面的参数

```
<script>
	function parseQueryString(input){
		var output;
		var qs =  input.split("?")[1];
		//保存数据的对象
		args = {};
		//取得每一项
		items = qs.length ? qs.split("&") : [],
		item = null,
		name = null,
		value = null;
		for (var i = 0; i < items.length; i++) {
			item = items[i].split('=');
			name = decodeURIComponent(item[0]);
			value = decodeURIComponent(item[1]);  //decodeURIComponent中文编码
			if(name.length){
				args[name] = value;
			}
		};
		return args;
	}
	var arr = parseQueryString('www.baidu.com?a=1&b=2');
	console.log(arr);
</script>
```
考察点：

* split
* 对解析字符串的理解
* 是否了解url 后面的格式，及是否考虑中文编码问题



###已知如下dom,点击li弹出文本节点内容,

```
<ul id="list">
    <li>pqge1</li>
    <li></li>
    <li></li>
    <li></li>
    <li></li>
    <li></li>
</ul>

function addEvent(elem, type, listener){
        if(elem.addEventListener){
            elem.addEventListener(type, listener, false);
        }else if(elem.attachEvent){
            elem[type+listener] = function(){
                listener.call(elem);
            };
            elem.attachEvent('on' + type, elem[type+listener]);

        }else{
            elem['on' + type] = listener;
        }
    }
    function removeEvent(elem, type, listener){
        if(elem.removeEventListener){
            elem.removeEventListener(type, listener, false);
        }else if(elem.detachEvent){
            elem.detachEvent('on' + type, elem[type+listener]);
        }else{
            elem['on' + type] = null;
        }
    }
    var aLi = document.getElementById('list').getElementsByTagName('li');
    for(var i=0; i<aLi.length; i++){
        addEvent(aLi[i], 'click', function(){
            console.log('--', this.innerHTML);
        });
    }
```
    
考察点：

* 事件绑定
* 时间委托


###写出下面输出的顺序

```
var deferred = function(fun){ //延迟
        return {
            done: function (fn) { //1
            	console.log(1);
                fun(function (data) {// callback  3
                	console.log(3);
                    fn(data);  //4
                });

            }
        };
    }
    var promise = deferred(function(callback){ //2
    	console.log(2);
    	setTimeout(function(){
    		callback('lalala');  //3
    	}, 2000);
    });
    promise.done(function(data){// fn  4
    	console.log(4);
    	console.log(data);
```

1,2,3,4,lalala

考察点：

* 回调
* 延迟函数


###jsonp

```
function jsonp(url, params, jsonpCallback){
        var head = document.getElementsByTagName('head')[0];
        var param = '';

        // 拼接请求信息
        for(var i in params){
            if(param == ''){
                param = i+'='+params[i];
            }else{
                param+= '&'+i+'='+params[i];
            }
        }
        var script = document.createElement('script');
        script.type = 'text/javascript';
        script.src = url + '?callback=' + jsonpCallback + '&' + param;
        if(head){
            head.appendChild(script);
        }else{
            document.body.appendChild(script);
        }
    }
    function fn () {
        alert('bububu')
    }
    jsonp('http://localhost:3000/maincloud/pages/about/$a', {}, 'fn')
```




###统计字符串中字符个数
```
var str = 'abbcccddd';
	var o = {};
	var key = '';
	var max = 0;
	for (var i = 0; i < str.length; i++) {
		if(!o[str[i]]){
			o[str[i]] = 1;
			if(max < o[str[i]]){
				key = str[i];
				max = o[str[i]];
			}
		}else{
			o[str[i]]++;
			if(max < o[str[i]]){
				key = str[i];
				max = o[str[i]];
			}
		}
	};
	console.log(o);
	console.log('key:' + key + ",max:" + max);
```


###写出结果
```
版本一
var a = 5;
	function test(){
		this.a = 10;
		a = 15;
		this.func = function(){
			var a = 20;
		}
	}
	var tt = new test();
	tt.func()
	setTimeout(tt.func, 1000);
	
版本二
function A(){
		this.a = 1;
		setTimeout(function(){
			this.a = 2;
			try{
				this.b = 'b';
				throw "";
			}
			catch(e){
				this.b = 'bb'
			}
		},0);
		this.b = 'bbb';

	}
	var aa = new A();
	setTimeout(function(){
		console.log(aa.a);
		console.log(window.a);
		console.log(aa.b);
		console.log(window.b);
	},0);	
	//1,2,bbb,b
```
	
考察点：
* this
* setTimeout this




###闭包的种类 
```
函数作为返回值
function fn () {
    return function () {
        return 1
    }
}
console.log(fn()())

函数作为参数
function fnc () {
    return 2
}
;(function (fn) {
    console.log(fn())
})(fnc)

```



```
add(5)(2)  => 7
function add(x) {
  return function(y) {
    return x + y;
  };
}

add1(2, 2)(3, 1)  => 8
//add1(...)(...)
function add1 () {

    let arg = Array.prototype.slice.call(arguments);

    return function () {
        let sum = 0;
        var v = Array.prototype.slice.call(arguments);
        v = v.concat(v[0])

        for(var i = 1, len = v.length; i < len; i++) {
            if(v[i]) {
                sum += v[i];
            }
        }
        return sum;
    }.bind(this, arg)
}
console.log('===', add1(2, 2)(3, 1))

function add2 () {
    let arg = Array.prototype.slice.call(arguments);
    return function call() {
        var ar = Array.prototype.slice.call(arguments);
        console.log('----1', ar)

        if(!ar[1]) {
            ar = ar.concat(ar[0])
            ar.shift()
            return function () {
                let sum = 0;
                var v = Array.prototype.slice.call(arguments);
                v = v.concat(v[0])

                for(var i = 1, len = v.length; i < len; i++) {
                    if(v[i]) {
                        sum += v[i];
                    }
                }
                return sum;
            }.apply(this, ar)
        }
        ar = ar.concat(ar[0])
        ar.shift()
        console.log('----2', ar)

        return call.bind(this, ar)
    }.bind(this, arg)
}
var add2 = function() {
var _this = this,
_args = arguments
return function() {
if (!arguments.length) {
var sum = 0;
for (var i = 0,
c; c = _args[i++];) sum += c
return sum
} else {
Array.prototype.push.apply(_args, arguments) return arguments.callee
}
}
}
// console.log('------', add2(1, 1)(2, 3, 1)(3)(4)(5)(20)(20)(30)(10)())






var name = 2;
var o = {
    name: 1,
    fn: function () {
        return function () {
            return this.name
        }
    }
}

console.log(o.fn()()) 输出

考察点：

* 闭包
* 上下文this 


```

###代码优化
```
function MyObject(name, message) {
  this.name = name.toString();
  this.message = message.toString();
  this.getName = function() {
    return this.name;
  };

  this.getMessage = function() {
    return this.message;
  };
}



优化为： 

function MyObject(name, message) {
    this.name = name.toString();
    this.message = message.toString();
}
(function() {
    this.getName = function() {
        return this.name;
    };
    this.getMessage = function() {
        return this.message;
    };
}).call(MyObject.prototype);
```




###var a=1; 与 a=1 的区别
var 声明变量
后者是一个赋值语句，给给全局window 创建一个属性



###质因数分解17735330000 为2^2 * 3^3 * 5^4 * 935 * 1861

(2**4)(5**4)(953)(1861)

写出算法



###asd\_ad\_bsdas\_csd\_asd\_dccds\_sdc\_ to Asd\_Ad\_Bsdas\_Csd\_Asd\_Dccds\_Sdc\_
```
var x = str.split('_').map(function (item) {
            return (item[0] ? item[0].toUpperCase() : '') + item.substring(1);
        }).join('_');
```


###bind 方法实现

###逆转矩阵
```
var arr = [];
for(var i = 0; i < 3; i++) {
    arr[i] = [];
}
arr[0].push(1,2,3)
arr[1].push(4,5,6)
arr[2].push(7,8,9)
console.log(arr)
for(var i = 0; i < 3; i++) {
    for(var j = 0; j < 3; j++) {
        if(i < j) {
            var v = arr[i][j];
            arr[i][j] = arr[j][i];
            arr[j][i] = v;
        }
    }
}
document.write(arr[0] + '<br/>' + arr[1] + '<br/>' + arr[2])
```



####说明为什么报错
```
function bar(x = y, y = 2) {
  return [x, y];
}

bar(); // 报错

```
考察点：

* es6 暂时性死区

* ES6 规定暂时性死区和let、const语句不出现变量提升，主要是为了减少运行时错误，防止在变量声明前就使用这个变量，从而导致意料之外的行为。

#### js 变量声明

考察点：

* ES5 只有两种声明变量的方法：var命令和function命令。ES6除了添加let和const命令，后面章节还会提到，另外两种声明变量的方法：import命令和class命令。所以，ES6 一共有6种声明变量的方法。
