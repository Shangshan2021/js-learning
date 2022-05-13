# The 11th week of learning JS

## [Learning videos](https://www.bilibili.com/video/BV1J4411Q7Fx?p=1)

### 1.34Message book

#### Demand

1. Name and content can be entered
2. After submission, the message will be displayed below
   1. If input is none, a prompt will be displayed.

#### Steps

1. Gets the input value and determines.
2. Create rows and print string.

#### Outcome

```html
<!DOCTYPE html><html lang="en" xmlns="http://www.w3.org/1999/xhtml">
<head>
    <meta charset="utf-8" />
    <title></title>
    <script>
        window.onload = function () {
            var oT = document.getElementById('text');
            var oC = document.getElementById('content');
            var oB = document.getElementById('btn');
            var oM = document.getElementById('message_text');
            var oUl = document.getElementById('fill_in');
            var oUl = oM.children[1];
            oB.onclick = function () {
                if (oT.value == '' || oC.value == '') {         //判断值是否为空
                    alert('数据为空'); return;
                }
                var oLi = document.createElement('li');
                oLi.innerHTML = '<h3>' + oT.value + '<h3><p>' + oC.value + '</p>';      //将输入内容用html语法打印
                if (oUl.children == 0) {
                    oUl.appendChild(oLi);
                }
                else {oUl.insertBefore(oLi,oUl.children[0])}
            }
        }
    </script>
</head>
<body>
    <div id="box">
        <ul id="fill_in">
            <li>姓名<input id="text" type="text"></li>
            <li>内容:<textarea id="content"></textarea></li>
            <li><input id="btn" type="button" value="提交"></li>
        </ul>
        <div id="message_text">
            <h2>显示留言</h2>
            <ul></ul>
        </div>
    </div>
</body>
</html>
```

#### Program analysis:

1. The new results, the new methods are already learned.
2. To save time, styles are not restored

### 1.35Realize the floating frame

#### Demand

1. A hover box appears at the bottom right of the page to the top

#### Steps

1. Gets the actual location on the page

   ```
   <!DOCTYPE html><html lang="en" xmlns="http://www.w3.org/1999/xhtml">
   <head>
       <meta charset="utf-8" />
       <title></title>
       <style>
           #div1{width:200px;height:200px;background-color:#ccc;border:1px;border-color:red;padding:50px;margin:50px;}
       </style>
       <script>
           window.onload = function () {
               var oDiv = document.getElementById('div1');
               alert(oDiv.offsetHeight);
           }
       </script>
   </head>
   <body>
       <div id="div1"></div>
   </body>
   </html>
   ```

#### Outcome

```html
<!DOCTYPE html><html lang="en" xmlns="http://www.w3.org/1999/xhtml">
<head>
    <meta charset="utf-8" />
    <title></title>
    <style>
        body{height:3000px;}
        #div1 {
            width: 200px;
            height: 200px;
            background-color: red;
            _top: 0;
            position:fixed;
            _position:absolute;
            bottom:0;
            right: 0;
        }
    </style>
    <script>
        window.onresize = window.onload = window.onscroll = function () {       //加事件,onscroll:滚动事件
            if (window.navigator.userAgent.indexOf('MSIE 6.0') != -1) {     //判断浏览器
                var oDiv = document.getElementById('div1');
                var sT = document.documentElement.scrollTop || document.body.scrollTop;     //浏览器兼容
                var cH = document.documentElement.clientHeight;     //可视区高度
                var oH = oDiv.offsetHeight;
                oDiv.style.top = sT + cH - oH + 'px';
            }
        }
    </script>
</head>
<body>
    <div id="div1">
    </div>
</body>
</html>
```



### 1.37Implement to-do lists

#### Demand

1. Click the button to add content. 
2. Click the newly added content to delete the newly added content

Outcome

```
<!DOCTYPE html><html lang="en" xmlns="http://www.w3.org/1999/xhtml">
<head>
    <meta charset="utf-8" />
    <title></title>
    <script>
        window.onload = function () {
            var oBtn = document.getElementById('btn');
            var oBox = document.getElementById('box');
            var oTxt = document.getElementById('text');
            var count = 0;
            oBtn.onclick = function () {
                if (oTxt.value == '') {
                    alert('内容不能为空');
                    return;
                }
                if (oBox.innerHTML == '') {
                    oBox.innerHTML = '<em>这里显示任务</em>';
                }
                count++;
                var oP = document.createElement('p');
                oP.innerHTML = count + '' + oTxt.value;
                oBox.append(oP);
                oTxt.Value = '';
                //插入任务之后,
                oP.onmouseover = function () {			//鼠标移入显示提示信息
                    this.style.background = 'yellow';
                    var oS = document.createElement('span');
                    oS.innerHTML = '确定删除<strong>' + this.innerHTML + '<strong>吗?';
                    oP.appendChild(oS);
                }
                oP.onmouseout = function () {		//移出时移除提示信息
                    this.style.background = '#f1f1f1';
                    this.removeChild(this.children[0]);
                }
                oP.onclick = function () {			//点击时删除任务
                    oBox.removeChild(this);
                    if (oBox.innerHTML == '') {
                        oBox.innerHTML = '<em>这里显示任务</em>';
                    }
                }
            }
        }
    </script>
</head>
<body>
    <div id="box"></div>
    <input type="text" id="text" />
    <input type="button" id="btn" value="提交">
</body>
</html>
```

- The comments are very clear and I won't go into them here

## 一些尝试

### JS连接数据库

- 在这之前要配制环境
  - 安装node & npm & cnpm
  - 用 `cnpm install mysql` 安装相关包
  - 再用`ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY '123456';FLUSH PRIVILEGES;`解决报错
  - 就可以运行下面的代码了

```Js
let mysql = require("mysql");
let options = {
    host: "localhost",
    port:"3306",
    user: "root",
    password: "123456",
    database:"JSearch"
}
//创建与数据库连接对象
let conn=mysql.createConnection(options);
//建立链接
conn.connect((err)=>{
    //失败则....
    if(err)console.log(err)
    else console.log("链接成功")
})

//执行语句
let strsql="select * from User";
conn.query(strsql,(err,results,fields)=>{
    console.log(err)
    console.log(results)
    console.log(fields)
})
```

结果如下:

```
链接成功
null
[ RowDataPacket { id: 1, name: 'sad' } ]
[
  FieldPacket {
    catalog: 'def',
    db: 'jsearch',
    table: 'User',
    orgTable: 'user',
    name: 'id',
    orgName: 'id',
    charsetNr: 63,
	.............(太多,就不放出来了)
```



这里有一个问题就是,所有的账号,密码都是未加密的,正大光明地给别人看,这是不行的

所以暂时放弃用JavaScript链接数据库

### Javascript实现搜索框自动提示

- `$`的用法:可以代替`document.getElementById`

#### 尝试一:

```js
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>搜索框提示</title>
    <style>
        * {
            margin: 0;
            padding: 0;
        }
 
        #searchbox {
            width: 300px;
            position: relative;
            margin: 100px;
            left: 40%;
        }
 
        #searchbox #hint {
            display: none;
            border: 1px solid gainsboro;
            width: 150px;
            height: 30px;
            position: absolute;
            top: -35px;
            border-radius: 5px;
        }
 
        #searchbox #hint::before {
            content: '';
            width: 0;
            height: 0;
            border: 5px solid rgb(219, 211, 211, .5);
            border-color: rgb(219, 211, 211, .5) transparent transparent;
            position: absolute;
            top: 30px;
            left: 50%;
            margin-left: -3px;
        }
 
        #searchbox #search {
            margin-top: 5px;
            height: 30px;
            padding: 5px;
        }
 
        #searchbox #search::placeholder {
            color: rgb(190, 173, 173);
        }
    </style>
    <script>
        window.onload=function(){
            var searchList=new Array();
            // 效果：输入内容显示提示框，获得焦点显示提示框，失去焦点隐藏提示框；内容为空不做提示
            // 获取事件源：hint search
            var hint = document.getElementById('hint');
            var search = document.getElementById('search');
            var btn = document.getElementById('btn');       
            var history = document.getElementById('history');       //打印历史记录
            var count=0;        //用于记录历史的条数,FIFO,超过十条删除最旧的
            // 使用事件流注册事件 处理程序
            // 1.键盘输入事件
            search.addEventListener('keyup', function () {
                if (search.value == '') {
                    hint.style.display = 'none';
                } else {
                    hint.style.display = 'block';
                    hint.innerHTML = searchList[0];
                }
            })
            // 2.获取焦点事件
            search.addEventListener('focus', function () {
                if (this.value !== '') {
                    hint.style.display = 'block';
                    hint.innerHTML = searchList[0];
                }
            })
            //3.失去焦点事件
            search.addEventListener('blur', function () {
                hint.style.display = 'none';
            })
            hint.onclick=function(){
                alert("OK");
            }
            btn.onclick=function(){
                if(search.value=='')alert("你什么都没有输入");
                else {
                    count++;
                    alert("这里没有你要的信息");
                    searchList.unshift(search.value);   //向前插入
                    var oP=document.createElement('p');
                    oP.innerHTML=count + '' + search.value;
                    history.append(oP);
                }
            }
        }
    </script>
</head>
 
<body>
    <div id="searchbox">
        <div id="hint"></div>
        <input type="search" name="" id="search" placeholder="请输入">
        <input type="button" id="btn" value="search">
    </div>
    <div id="history">

    </div>
</body>
 
</html>
```

- 其实焦点事件会在视频学习的46期出现
- 现在简单实现了一下,还缺少
  - Enter事件搜索
  - 展示多条语句
  - style的设计
  - 提示框点击事件

