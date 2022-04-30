# The ninth week of learning JS

## [Learning videos](https://www.bilibili.com/video/BV1J4411Q7Fx?p=1)

### 1.20Timer

#### Demand

1. Pop up 1 every other second

#### Steps

1. Two possibilities for managing timer:

   1. `setInterval`:Repeat at regular intervals: clock

      ```
      	<script>
              setInterval(function () {
                  alert(1);
              },1000)
          </script>
      ```

   2. `setTimeout`:Do it once in a while: timebomb

      ```
      <script>
              setTimeout(function () {
                  alert(1);
              },1000)		//Execute only once
          </script>
      ```

2. Add middleware so that the units digit is preceded by 0

   ```
   function tuDou(n) {
                   return n < 10 ? '0' + n : '' + n;
               }
   ```

3. Close and then open a new one:

   ```
   var timer = setInterval(function (){....},time)
   clearInterval(timer);
   ```

#### Outcome

```
<!DOCTYPE html><html lang="en"><head><meta charset="UTF-8"><title>Title</title>
    <script>
        window.onload = function () {
            var Time = document.getElementById('time');
            var Start = document.getElementById('start');
            var Stop = document.getElementById('stop');
            var timer = null;
            function tuDou(n) {
                return n < 10 ? '0' + n : '' + n;
            }
            Start.onclick = function () {
                var s = 0;
                clearInterval(timer);
                timer = setInterval(function () {
                    s++;
                    Time.value = tuDou(parseInt(s/60))+':'+tuDou(s%60);
                }, 50)
            }
            Stop.onclick = function () { clearInterval(timer); }
        }
    </script>
</head>
<body>
    <input type="text" value="00:00" id="time" >
    <input type="button" value="开始" id="start" >
    <input type="button" value="暂停" id="stop" >
</body>
</html>
```

#### Program analysis:

1. Simple, needless to say
2. Maybe we can do a continuing function button
   1. The implementation is also simple, reserving the value when pausing and adding from this value when clicking continue button.

### 1.23Autoplay TAB

#### Demand

1. Pop up 1 every other second

#### Steps

1. Create tabs
2. Manual play TAB
3. Autoplay TAB

#### Outcome

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <style>
        #box .on{
            background:red;
        }
        #box div{
            width:200px;
            height:200px;
            display:none;
            border:1px solid red;
        }
    </style>
    <script>
        window.onload = function () {
            var Box = document.getElementById('box');
            var Btn = Box.getElementsByTagName('input');
            var Div = Box.getElementsByTagName('div');
            var Prev = document.getElementById('prev');
            var Next = document.getElementById('next');
            var Num_now = 0;
            var timer = null;

            function table() {
                for (var i = 0; i < Btn.length; i++) {
                    Btn[i].className = '';
                    Div[i].style.display = 'none';
                }
                Div[Num_now].style.display = 'block';
                Btn[Num_now].className = 'on';
            }

            for (var i = 0; i < Btn.length; i++) {
                Btn[i].index = i;
                Btn[i].onclick = function () {
                    Num_now = this.index;
                    table();
                }
            }

            timer = setInterval(function () {
                fNext();
            }, 500);

            Box.onmouseover = function () {
                clearInterval(timer);
            }

            Box.onmouseout = function () {
                timer = setInterval(function () {
                    fNext();
                }, 500);
            }

            function fNext() {
                Num_now = (Num_now + 1) % 3;
                table();
            }

            Next.onclick = fNext();

            Prev.onclick = function () {
                Num_now = (Num_now + 2) % 3
                table();
            }

        }
    </script>
</head>
<body>
    <div id="box">
        <a href="javascript:;" id="prev"> <- </a>
        <input type="button" value="f1" class="on">
        <input type="button" value="f2" class="on">
        <input type="button" value="f3" class="on">
        <a href="javascript:;" id="next"> -> </a>
        <div style="display:block">f1</div>
        <div>f2</div>
        <div>f3</div>
    </div>
</body>
</html>
```

#### Program analysis:

1. For better results, consider changing the judgement region of onMouse

## Question(x)

## Solution

## About Node.js

1. 与Python中的Django很类似,这里附上Django的学习[链接](https://django-learning.readthedocs.io/en/latest/)
2. ![img1.20](.\pic\img1.20.png)

