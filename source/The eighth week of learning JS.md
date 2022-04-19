# The eighth week of learning JS

## [Learning videos](https://www.bilibili.com/video/BV1J4411Q7Fx?p=1)

### 1.18 Function return value

#### Demand

1. Generate random numbers from 5 to 10

#### Steps

1. Two possibilities for returning an undefined error:
   1. No return value as the function exit.
   2. Has return ,but is empty.
2. Random number generation
   1. `n+Math.random()*m`
   2. n为下边界,m为差
3. Review format conversion
   1. `ParseInt`转换为整形

#### Outcome

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <script>
        function rnd(n, m) {
            return n + parseInt(Math.random()*(m-n));
        }
        alert(rnd(5,15));
    </script>
</head>
<body>

</body>
</html>
```

Program analysis:

1. Basic, needless to say

### 1.19 JDcom  UnionLotto

#### Demand

1. Generates a random set of non-repeating integers between 1 and 33

#### Steps

1. Generate random numbers from 1 to 33
2. Generate seven numbers 
3. Add a judgment condition
4. `arr.push()`This shows that arrays in JS are stored on the stack

#### Outcome

Without watching the video

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <script>
        function rnd(n, m) {
            return n + parseInt(Math.random()*(m-n));
        }
        var arr = [];
        for (var i = 0; i < 7; i++) {
            var iNum = rnd(1, 34);
            var key=1
            for (var j = 0; j < arr.length; j++) {
                if (iNum == arr[j]) {
                    i--;
                    key = 0;
                    alert(iNum);
                    break;
                }
                else continue;
            }
            if (key == 1) {
                arr[i] = iNum;
                document.write(iNum);
                document.write("<br>");
            }
        }
    </script>
</head>
<body></body>
</html>
```

After watching:

```html
<!DOCTYPE html><html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <script>
        function rnd(n, m) {
            return n + parseInt(Math.random()*(m-n));
        }
        var arr = [];
        function findRepeat(num, array) {
            for (var j = 0; j < array.length; j++) {
                if (num == array[j]) {
                    return false;
                }
            }
            return true;
        }
        for (var i = 0; i < 7; i++) {
            var iNum = rnd(1, 34);
            if (findRepeat(iNum, arr)) {
                arr[i] = iNum;
                document.write(iNum);
                document.write("<br>");
            }
            else i--;
        }
    </script>
</head>
<body></body>
</html>
```

Program analysis:

1. Using functions simplifies the process,Thinking is clearer.
2. Using Ternary operator can reduce redundant conditional statements:`condition ? x : y`

## Question(x)

## Solution(x)

## Edit

转载自菜鸟编程:

```html
<!DOCTYPE html>
<html lang="en">
<head><meta charset="UTF-8"><title>Title</title>
    <style>
        #myInput {
            background-image: url('https://static.runoob.com/images/mix/searchicon.png'); /* 搜索按钮 */
            background-position: 10px 12px; /* 定位搜索按钮 */
            background-repeat: no-repeat; /* 不重复图片*/
            width: 100%;
            font-size: 16px; /* 加大字体 */
            padding: 12px 20px 12px 40px;
            border: 1px solid #ddd;
            margin-bottom: 12px;
        }
        #myUL {
            /* 移除默认的列表样式 */
            list-style-type: none;
            padding: 0;
            margin: 0;
        }
        #myUL li a {
            border: 1px solid #ddd; /* 链接添加边框 */
            margin-top: -1px;
            background-color: #f6f6f6;
            padding: 12px;
            text-decoration: none;
            font-size: 18px;
            color: black;
            display: block;
        }
        #myUL li a.header {
            background-color: #e2e2e2;
            cursor: default;
        }
        #myUL li a:hover:not(.header) {
            background-color: #eee;
        }
    </style>

    <script>
        function myFunction() {
            // 声明变量
            var input, filter, ul, li, a, i;
            input = document.getElementById('myInput');
            filter = input.value.toUpperCase();
            ul = document.getElementById("myUL");
            li = ul.getElementsByTagName('li');
            // 循环所有列表，查找匹配项
            for (i = 0; i < li.length; i++) {
                a = li[i].getElementsByTagName("a")[0];
                if (a.innerHTML.toUpperCase().indexOf(filter) > -1) {
                    li[i].style.display = "";
                } else {
                    li[i].style.display = "none";
                }
            }
        }
    </script>
</head>
<body>
    <input type="text" id="myInput" onkeyup="myFunction()" placeholder="搜索...">

    <ul id="myUL">
        <li><a href="#" class="header">A</a></li>
        <li><a href="#">Adele</a></li>
        <li><a href="#">Agnes</a></li>

        <li><a href="#" class="header">B</a></li>
        <li><a href="#">Billy</a></li>
        <li><a href="#">Bob</a></li>
        
        <li><a href="#" class="header">C</a></li>
        <li><a href="#">Calvin</a></li>
        <li><a href="#">Christina</a></li>
        <li><a href="#">Cindy</a></li>
    </ul>
</body>
</html>
```

#### 程序分析

1. 关于调用
   1. `.toUpperCase()`用于转换为大写(filter和li表格),方便查询相同字母
   2. `indexOf()`用于找出相似的
2. 这里的难点在于如何产生下拉框,并一条条列出符合条件选项,且有上限
   1. 自己写时用了数组,也实现了查找相关项
   2. 而上面的代码则是避开了这一点,用表格每行的显示与否来代替下拉框

#### 改进(待续)

