# The fifth week of learning JS

## [Learning videos](https://www.bilibili.com/video/BV1J4411Q7Fx?p=1)

### 1.11 How Realize the reverse selection function?

#### Demand

1. In advanced week,we have realized the function of all selecting,So we only have to perform Not operations.

#### Steps

1. Two ways to reverse:
   1. Boolean non operator:`!`,! true = false;! false = true
   2. Xor operator:`^` 1 ^ 1 = 0;0 ^ 1 = 1

#### Outcome

##### Without watching the video

```html
<!DOCTYPE html><html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <script>
        window.onload=function(){
            var ele_2=document.getElementById('btn1');
            var ele_m=document.getElementsByTagName('input');
            ele_2.onclick=function(){
                //for(i=0;i<5;i++){ele_m[i].checked=!ele_m[i].checked;}
                for(i=0;i<5;i++){ele_m[i].checked=1^ele_m[i].checked;}
            }
        }
    </script>
</head>
<body>
    <button type="button" id="btn1">reserve select</button>
    <hr>
    <input type="checkbox" name="a" id="cb1">
    <input type="checkbox" name="b" id="cb2">
    <input type="checkbox" name="c" id="cb3">
    <input type="checkbox" name="d" id="cb4">
</body>
</html>
```

Program analysis:

1. the resulting code is almost identical.Here no longer say.
2. Learning C really helps a lot.

### 1.12 Collection of three kinds of choosing

#### Outcome(Just a review)

```html
<!DOCTYPE html><html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <script>
        window.onload=function(){
            var ele_1=document.getElementById('btn0');
            var ele_2=document.getElementById('btn1');
            var ele_3=document.getElementById('btn2');
            var ele_m=document.getElementsByTagName('input');
            ele_1.onclick=function(){for(i=0;i<5;i++){ele_m[i].checked=true;}}
            ele_2.onclick=function(){for(i=0;i<5;i++){ele_m[i].checked=!ele_m[i].checked;}}
            ele_3.onclick=function(){for(i=0;i<5;i++){ele_m[i].checked=false;}}
        }
    </script>
</head>
<body>
    <button type="button" id="btn0">all select</button>
    <button type="button" id="btn1">reserve select</button>
    <button type="button" id="btn2">non select</button>
    <hr>
    <input type="checkbox" name="a" id="cb1">
    <input type="checkbox" name="b" id="cb2">
    <input type="checkbox" name="c" id="cb3">
    <input type="checkbox" name="d" id="cb4">
</body>
</html>
```

### 1.13 Linkage to choose

#### Demand

1. When the parent box is checked, the child box changes.
2. When all the child box is checked,the parent box checked.
3. If some child boxes have not been checked,the parent box would not be checked.

#### Outcome

```html
<!DOCTYPE html><html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <script>
        window.onload=function(){
            //Define variables
            var ele_p=document.getElementById('p_cb');
            var ele_b=document.getElementById('box');
            var ele_s=ele_b.getElementsByTagName('input');
            //set parent check box
            ele_p.onclick=function(){
                for(i=0;i<3;i++){
                    ele_s[i].checked=ele_p.checked;
                }
            }
            //set child check box
            for(i=0;i<3;i++){
                ele_s[i].onclick=function(){        //click - check true count
                    var count=0; 
                    for(i=0;i<3;i++){
                        if(ele_s[i].checked){count++;}
                    }
                    if(count==3){ele_p.checked=true;}
                    else{ele_p.checked=false;}
                }
            }
        }
    </script>
</head>
<body>
    <input type="checkbox" name="a" id="p_cb">
    <hr>
    <div id="box">
        <input type="checkbox" name="b" id="cb2">
        <input type="checkbox" name="c" id="cb3">
        <input type="checkbox" name="d" id="cb4">
    </div>
</body>
</html>
```

Program analysis:

1. Loop nesting is used here to traverse every child check box when chick any one of them.
2. Using simple statements and calls to realize different functions is amazing.

## Question

### 如果在点击事件中改变选框checked属性会如何?

```html
<!DOCTYPE html><html lang="en"><head><meta charset="UTF-8"><title>Title</title>
    <script>

        window.onload=function(){
            var ele_p=document.getElementById('p_cb');
            var ele_b=document.getElementById('box');
            var ele_s=ele_b.getElementsByTagName('input');

            ele_p.onclick=function(){for(i=0;i<ele_s.length;i++){ele_s[i].checked=ele_p.checked;}}

            for(i=0;i<ele_s.length;i++){
                ele_s[i].onclick=function(){
//---------------------------------------------------------
                    ele_s[i].checked=true;		//add
//---------------------------------------------------------
                    var count=0;
                    for(i=0;i<ele_s.length;i++){
                        if(ele_s[i].checked){count++;}
                    }
                    if(count==ele_s.length){ele_p.checked=true;}
                    else{ele_p.checked=false;}
                }
            }
        }
    </script>
</head><body>
    <input type="checkbox" name="a" id="p_cb">
    <hr>
    <div id="box">
        <input type="checkbox" name="b" id="cb2"><input type="checkbox" name="c" id="cb3"><input type="checkbox" name="d" id="cb4">
    </div>
</body></html>
```

​	仅仅添加了一行,看似不会有影响的代码,由下至上的联选功能却不可用了.