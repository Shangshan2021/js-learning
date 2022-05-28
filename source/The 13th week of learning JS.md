# The 13th week of learning JS

## [Learning videos](https://www.bilibili.com/video/BV1p4411Q7pT?p=1)

### 关于跨域

#### 一、什么是跨域？

​		在了解跨域之前，首先要知道什么是同源策略（same-origin policy）。简单来讲同源策略就是浏览器为了保证用户信息的安全，防止恶意的网站窃取数据，禁止不同域之间的JS进行交互。对于浏览器而言只要域名、协议、端口其中一个不同就会引发同源策略，从而限制他们之间如下的交互行为：

1.Cookie、LocalStorage和IndexDB无法读取；

2.DOM无法获得；

3.AJAX请求不能发送。

​		跨域的严格一点的定义是：只要协议，域名，端口有任何一个的不同，就被当作是跨域。

#### 二、为什么浏览器要限制跨域访问呢？

​		原因就是安全问题：如果一个网页可以随意地访问另外一个网站的资源，那么就有可能在客户完全不知情的情况下出现安全问题。比如下面的操作就有安全问题：

1.用户访问www.mybank.com，登陆并进行网银操作，这时cookie啥的都生成并存放在浏览器；

2.用户突然想起件事，并迷迷糊糊的访问了一个邪恶的网站www.xiee.com；

3.这时该网站就可以在它的页面中，拿到银行的cookie，比如用户名，登陆token等，然后发起对www.mybank.com的操作；

4.如果这时浏览器不予限制，并且银行也没有做响应的安全处理的话，那么用户的信息有可能就这么泄露了。

#### 三、为什么要跨域？

​		既然有安全问题，那为什么又要跨域呢？ 有时公司内部有多个不同的子域，比如一个是location.company.com ,而应用是放在app.company.com , 这时想从 app.company.com去访问 location.company.com 的资源就属于跨域。

### 四、解决跨域问题的方法：

1.跨域资源共享（CORS）

2.通过jsonp跨域



————————————————————————

**由于此文描述比视频更为全面，所以笔记直接参考了相关文章。**

————————————————————————
版权声明：上文为CSDN博主「luckylareina」的原创文章。
原文链接：https://blog.csdn.net/lareinalove/article/details/84107476



### Jsonp实现百度搜索

##### 代码实现

```css
<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="UTF-8">
        <title>Document</title>
        <script>
            function show(json){
                var oUl=document.getElementById('ul1');
                oUl.innerHTML='';
                var arr=json.s;
                for(var i=0;i<json.s.length;i++){
                    var oLi=document.createElement('li');
                    oLi.innerHTML=arr[i];
                    oUl.appendChild(oLi);
                }
            }
        </script>
        <script>
            function jsonp(url){
                var oScript=document.createElement('script');
                oScript.src=url;
                document.head.appendChild(oScript);
            }
        </script>
        <script>
            window.onload=function(){
                var oTxt=document.getElementById('text1');
                oTxt.onkeyup=function(){
                    jsonp
                    ('https://sp0.baidu.com/5a1Fazu8AA54nxGko9WTAnF6hhy/su?wd='+oTxt.value+'&cb=show');
                }
            }
        </script>
    </head>
    <body>
        <input type="text" placeholder="请输入关键字" id="text1">
        <ul id="ul1">
            <li>jdaisoj</li>
        </ul>
    </body>
</html>
```

因为已经在之前周的学习中实现过了搜索框提示，所以这个例子并不难。

主要是提供了一种新思路，借用其他网站的相关搜索或计算结果，取得其Json值，本网页只用读取并输出即可。

## 一些尝试

1. 大体上功能已经齐全，现在缺少一个记录搜索的文件，最后尝试实现一下这个
2. 如果可以，还能再嵌入一个百度搜索按钮，用这节课所学
3. 改进了`回车`搜索后的代码

​		

```
<html>
<head>
    <meta charset="UTF-8">
    <title>个人搜索页面</title>
    <style>
        @font-face {
            font-family:myFont;
            src: url(FZYanZQKSJF.TTF);
        }
        html,body{
	        height: 100%;
        }
        .background{
            position: fixed;
            width: 100%;
            height: 100%;
            left: 0;
            top: 0;
            font-family:myFont;
        }
        .searchbox{
            box-sizing: border-box;
            min-height: 40px;
            max-height: 52px;
            min-width: 580px;
            max-width: 596px;
            white-space: nowrap;
            position: absolute;
            top: 25%;
        }
        .searchinput{
            width: 600px;
            height: 52px;
            border-radius:30px ;
            margin: auto;
            position: relative;
            left: 35%;
            font-size:20px;
            background-color:#eea2a4;
            padding: 12px 10px 12px 16px;
            font-family:myFont;
        }
        .options{
            height: 25%;
            width: 100%;
        }
        body{
            background: url('Jsearch.png') no-repeat center/cover;
        }
        .searchbutton{
            position: relative;
            top:20px;
            left: 680px;
            height: 52px;
            width: 52px;
        }
        .searchlist{
            position: relative;
            left: 36%;
            top:0px;
        }
        p{
            background-color:#93b5cf;
            height: 25px;
            width:540px;
            border-radius:30px ;
            font-size:20px;
            padding: 12px 10px 12px 16px;
        }
    </style>
    <script type="text/javascript">
        window.onload=function(){
            var form = document.getElementById("form");
            var input1 = document.getElementById("input1")
            var wrap = document.getElementById("wrap");
            var btn=document.getElementById("btn");
            var count=0;
            var history = document.getElementById('history');
            var arr1 = [];//数组里面的元素就是我希望在输入宽输入某个字符后在下方出现的搜索字符。
            var arr2 = [];//这个数组是为了装入经过筛选和匹配符合要求的arr1中的元素。
            input1.addEventListener("keyup", function(event) {
                    event.preventDefault();
                    if (event.keyCode === 13) {
                        btn.click();
                    }
                });
            input1.oninput = function() {
                var val = input1.value;//获取当前输入框的值。
                arr2 = [];//使得每次输入框值变化后数组arr2为空。否则wrap中的元素会越来越多。
                var p1 = wrap.getElementsByTagName("p");
                for (var k = p1.length-1; k >= 0; k--) {
                    p1[k].remove();
                };
                //装入筛选后字段
                for (var i = 0, max = arr1.length;i<max; i++) {     //这样做好像可以减少调用负担
                    if (arr1[i].indexOf(val) > -1 ) {
                        arr2.push(arr1[i]);
                    }   
                }
                //创建元素的循环。在每个创建的元素内添加arr2数组中的字符串。
                for (var j = 0; j < arr2.length; j++) {
                    var p = document.createElement("p");
                    var a = document.createElement("a");
                        a.innerText = arr2[j];
                        a.setAttribute("href","https://cn.bing.com/search?q="+arr2[j]);
                        p.appendChild(a);
                        wrap.appendChild(p);
                }
            }
            btn.onclick=function(){
                var val = input1.value;//获取当前输入框的值。
                if(val=='')alert("你还什么都没有输入!")
                else {
                    arr1.unshift(val);
                    count++;
                    console.log(count);
                    if(count>3)arr1.splice(4,1);
                    var jump = confirm("这里没有你要的信息,请前往谷歌搜索");
                    if(jump) parent.location='https://www.google.com.hk/search?q='+val;
                }
                for (var i = 1, max = arr1.length;i<max; i++) {
                    if (arr1[i]==val) {
                        arr1.splice(i,1);
                    }   
                }
            }
        }
    </script>
</head>
<body class="mainbody" >
    <div class="background">
        <div id="history" class="options"></div>
        <div id="searchbox">
            <div id="form" name="form">
                <div>
                    <input type="text" class="searchinput" id="input1" onkeydown="keyup_submit(event);">
                    <img type="button" src="S.svg" id="btn" class="searchbutton">
                </div>
                <div id="wrap" class="searchlist"></div>
            </div>
        </div>   
    </div>   
</body>
</html>
```

