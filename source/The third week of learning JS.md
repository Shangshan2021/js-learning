# The third week of learning JS

## [Learning videos](https://www.bilibili.com/video/BV1J4411Q7Fx?p=1)

### 1.8 Extract inter-row events

#### Demand

1. click button,alert 1

#### Steps

1. There are many errors in the steps demonstrated in the video, not only in logic but also in syntax.That's   not good for readers to copy his code without thinking.

2. ```html
   <!DOCTYPE html>
   <html>
   <head>
   <meta charset="utf-8">
   <title>js-learning</title>
       <script>
           var var_ele=document.getElementById('btn');
           var_ele.onclick=show;
                function show(){
                   alert(1)
                }
       </script>
   </head>
   <body>
       <button type="button" id="btn">alert</button>
   </body>
   </html>
   ```

3. Html and JS will execute from top to bottom,`var_ele=document.getElementById('btn')` needs "btn" before `<button type="button" id="btn">`loaded "button:btn".

#### Outcome

```html
<!DOCTYPE html>
<html>
<head>
<meta charset="utf-8">
<title>js-learning</title>
    <script>
    window.onload = function (){
            var var_ele=document.getElementById('btn');
            var_ele.onclick=function (){
                    alert(1);
            };
    }
    </script>
</head>
<body>
    <button type="button" id="btn">alert</button>
</body>
</html>
```

#### Program analysis:

1. The function must be added after the event.

2. If add "()" to the function_Name after event ,the function will be executed at once.

3.  Verification possibility is important for learning program(In JS ,we can use `log` )

4. Definition of anonymous functions: 

   ```
   window.onload = function (){
   	alert(load competed);
   }
   ```

## My instance

```HTML
<!DOCTYPE html><html><head><meta charset="utf-8">
<title>js-learning</title>
    <style>
        #div1{
            width:200px;
            height:200px;
            background:black;
            }
    </style>
    <script>
        var key=0;
        window.onload=function (){
            document.getElementById('btn').onclick=function (){
                key=key^1;
                if(key==1){
                    alert("size is changing");
                    document.getElementById('div1').style.width='400px';
                };
            };
        }
    </script>
</head>
<body>
    <button type="button" id="btn">change size</button>
    <div id="div1"> </div>
</body></html>
```

#### Program analysis:

1. It's a pretty simple instance,however it contains all I have learned in those lessons:anonymous functions;conditional statement,the relationship between statement and event;variables;functions....
2. But there is a problem.I was going to change the div bigger and bigger,after pressing the button again and again,and I found that I couldn't change the number of width px ,I can only change it into "400px".Maybe this will talk about later.