# The first week of learning JS

## [Learning videos](https://www.bilibili.com/video/BV1J4411Q7Fx?p=1)

### 1.1 Javascript introduction

#### What is Javascript？

1. HTML:超文本标记语言,to create static web page.(Define the `content` of a web page)

   ```html
   <!DOCTYPE html>
   <html>
   <head>
      <title>My title</title>
   </head>
   <body>
      <h1>title</h1>
      <p>A sample</p>
   </body>
   </html>
   ```

2. CSS:A Cascading style sheet,helps style web pages.(Describe the `layout` of a web page)

   ```css
   <!DOCTYPE html>
   <html>
   <head>
   <meta charset="utf-8"> 
   <title>菜鸟教程(runoob.com)</title> 
       <style>
       body{background-color:#b0c4de;}
       </style>
   </head>
   <body>
   <h1>我的 CSS web 页!</h1>
   <p>你好世界！这是来自 runoob 菜鸟教程的实例。</p>
   </body>
   </html>
   ```

3. Javascript:(Control the `behavior` of a web page)

#### About structure , layout and behavior

- [Has been mentioned above]

#### Java and JavaScript

- Java is an object-related programming language
- Have nothing to do with each other

### 1.2 The first JavaScript program

- Example1

```html
<!DOCTYPE html>
<html>
<head>
<meta charset="utf-8">
<title>js-learning</title>
    <script>
    function displayDate(){document.getElementById("demo").innerHTML=Date();}
    </script>
</head>
<body>
    <h1>My first JavaScript program</h1>
    <p id="demo">When click{do display.}</p>
    <button type="button" onclick="displayDate()">show me the date</button>
</body>
</html>
```

- Example2

```html
<!DOCTYPE html>
<html>
<head>
<meta charset="utf-8">
<title>js-learning</title>
</head>
<body>
    <button type="button" onclick="alert(1)">show me the 1</button>
</body>
</html>
```

- Example3

```html
<!DOCTYPE html>
<html>
<head>
<meta charset="utf-8">
<title>js-learning</title>
    <style>
        #div1{
            width:100px;
            height:100px;
            background:red;
            display:none;
            }
    </style>
</head>
<body>
	<!--
    <button type="button" onclick="div1">show me the div</button>	//wrong!
    <div id="div1"></div>       
    The right way is to Change the `display` property to `block` ,like css.
    -->
    <button type="button" onclick="div1.style.display='block'">show me the div</button>
    <div id="div1"></div>
</body>
</html>
```

1. Program analysis:
   1. `onclick="instance_function()"` when click event occurs,execute instance_function.
   2. The content inside mast be a statement of behavior,however, 'div1' is just an element so it can't be recognize.
   3. incompatibility problem: `onclick="div1.style.display=' block' "` --- `document.getElementById('div1').style.display="block"`

### 1.3 Realize the mouse slide control hidden

- Example1

```html
<!DOCTYPE html>
<html><head><meta charset="utf-8"><title>js-learning</title>
    <style>
        #div1{
            width:100px;
            height:100px;
            background:red;
            }
    </style>
</head>
<body>
    <div id="div1" onmouseover="document.getElementById('div1').style.width='200px';document.getElementById('div1').style.height='200px'"
         onmouseout="document.getElementById('div1').style.width='100px';document.getElementById('div1').style.height='100px'"></div>
</body>
</html>
```

1. Program analysis:
   1. How to simplify the expression?
   2. Notice: Using ";" to separate two expression in one statement

### 1.4 Variables and functions

Example

```html
<!DOCTYPE html>
<html>
<head>
<meta charset="utf-8">
<title>js-learning</title>
    <style>
        #div1{
            width:100px;
            height:100px;
            background:red;
            }
    </style>
    <script>
        function toBig(){
        document.getElementById('div1').style.width='200px';
        document.getElementById('div1').style.height='200px';
        }
        function toSmall(){
        document.getElementById('div1').style.width='100px';
        document.getElementById('div1').style.height='100px';
        }
    </script>
</head>
<body>
	<!--
    css style is way to simplify expression.
    <script>tag is the way js to simplify expression.
    1.Define:row 13~22
    2.Invoke:row 31
    -->
    <div id="div1" onmouseover="toBig()" onmouseout="toSmall()"></div>
</body>
</html>
```

By using variables to simplify :

```html
   <script>
        function toBig(){
        document.getElementById('div1').style.width='200px';
        document.getElementById('div1').style.height='200px';
        }
        function toSmall(){
        document.getElementById('div1').style.width='100px';
        document.getElementById('div1').style.height='100px';
        }
    </script>
    --------------------------------------------------------------------------------------
    --------------------------------------------------------------------------------------
   <script>
        function toBig(){
        var_ele=document.getElementById('div1');
        var_ele.style.width='200px';
        var_ele.style.height='200px';
        }
        function toSmall(){
        var_style=document.getElementById('div1').style;
        var_style.width='100px';
        var_style.height='100px';
        }
    </script>
```

Program analysis:

1. Clearly,we can use variables to take place  `document.getElementById('div1')` or `document.getElementById('div1').style`.But,It's infeasible if you want to impact property.

2. Notice: There are some keywords that can't be used to name variables such as "var"

3. Variables and functions

   ```
   function functionName(){
   	......;
   	......;
   }
   ```

   ```
   varName=......
   ```

### 1.5 Conditional statement

```html
<!DOCTYPE html>
<html>
<head>
<meta charset="utf-8">
<title>js-learning</title>
    <style>
        #div1{
            width:100px;
            height:100px;
            background:red;
            display:none;
            }
    </style>
    <script>
        function showHide(){
            var_ele=document.getElementById('div1').style;
            if(var_ele.display=="none"){var_ele.display='block';}
            else{var_ele.display='none';}
        }
    </script>
</head>
<body>
    <button type="button" onclick="showHide()">hide the div</button>
    <div id="div1"></div>
</body>
</html>
```

Program analysis:

1. The grammar of Jscript if-conditional is just like C++'s .Here No Longer Say.





