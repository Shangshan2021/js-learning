# The fourth week of learning JS

## [Learning videos](https://www.bilibili.com/video/BV1J4411Q7Fx?p=1)

### 1.9 Extract inter-row events

#### Demand

1. click button,select all of the checkbox

#### Steps

1. code redundancy and it's not easy to maintain.Actrually,I know that the problem can be solved by parament,however,he offers a better way.

2. ```
   <script>
           window.onload=function(){
               var ele_1=document.getElementById('btn');
               var ele_2=document.getElementById('cb1');
               var ele_3=document.getElementById('cb2');
               var ele_4=document.getElementById('cb3');
               var ele_5=document.getElementById('cb4');
               ele_1.onclick=function(){
                   ele_2.checked=true;
                   .......				//too much
               }
           }
       </script>
   ```

3. `getElementsByTagName()` can reduce the define statements of the same kind of elements.

   ```
   <script>
           window.onload=function(){
               var ele_1=document.getElementById('btn');
              var ele_m=document.getElementsByTagName('input');
               ele_1.onclick=function(){
                   ele_m[0].checked=true;
                   .......				
               }
           }
       </script>
   ```

4. But I think that can be simplified even further. As we can use conditional statement,maybe we also can use loop  statement.

#### Outcome

```
<!DOCTYPE html><html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <script>
        window.onload=function(){
            var ele_1=document.getElementById('btn');
            var ele_m=document.getElementsByTagName('input');
            ele_1.onclick=function(){
                for(i=0;i<5;i++){ele_m[i].checked=true;}
            }
        }
    </script>
</head>
<body>
    <button type="button" id="btn">select all</button>
    <hr>
    <input type="checkbox" name="a" id="cb1">
    <input type="checkbox" name="b" id="cb2">
    <input type="checkbox" name="c" id="cb3">
    <input type="checkbox" name="d" id="cb4">
</body>
</html>
```

Program analysis:

1. The loop is just like C. It's easy to write exactly .
2. The difficulty lies on the kinds of elements in web should be  perfectly matched,every native function has its limit on element type.

#### Question

1. Maybe there is one function can return the count of the number of the elements,it will help to make the code more logical.

### 1.10  Two ways to manipulate content and properties

####  Change properties

1. One is to use `.` Just like Java or any kind of language that support object.
2. The other is to use `[]`,

#### Change content

1. Form elements:`element.value='xxxxx';`
2. Non-form elements:`element.innerHtml='xxxxx'`

#### Outcome

```html
<!DOCTYPE html><html><head><meta charset="utf-8">
<title>js-learning</title>
    <script>
        window.onload=function(){
            var ele=document.getElementById('btn')
            ele.onclick=function(){
                var bg='background';
                //ele.value="change content";
                //ele.innerHtml='change content';  this is for non-form elements
                //ele.style.background='red';       One way
                ele['style'][bg]='green';         //The other
            }
        }
    </script>
</head>
<body>
    <input type="button" value="change color" id="btn">
</body>
</html>
```

#### Program analysis:

1. Use `.` can increase readability. Nobody wants to look at a line of code and look up what the variable means.

