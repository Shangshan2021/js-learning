# The sixth week of learning JS

## [Learning videos](https://www.bilibili.com/video/BV1J4411Q7Fx?p=1)

### 1.14 Tab control

#### Demand

1. click button,show different div.

#### Steps

1. When we try to use variables in the For loop directly,There will be errors that you don't get the results you want.

```html
for(var i=0;i<aBtn.length;i++){
                aBtn[i].onclick=function(){aBtn[i].className='on';}
            }
```

2. This is because, whenever we click, the loop is complete and the variable is no longer specified by the click. To  solve it,we can use `this` to substitute the one we just orperated.

```html
for(var i=0;i<aBtn.length;i++){
                aBtn[i].onclick=function(){this.className='on';}
            }
```

3. We can use custom properties when the support properties do not meet the requirements.

```html
for(var i=0;i<aBtn.length;i++){
------------------------------------------------------
	aBtn[i].num=i;		//add
------------------------------------------------------
    aBtn[i].onclick=function(){
        for(var i=0;i<aBtn.length;i++){
            aBtn[i].cllassName='';
            aDiv[i].style.display="none";
        }
		this.className='on';
		aDiv[this.num].style.display="block";		//use
	}
}
```

#### Outcome

```html
<!DOCTYPE html><html lang="en"><head><meta charset="UTF-8"><title>Title</title>
    <style>
        .on{background: red;}
        div{width: 300px;height: 300px;border: 1px solid red;display: none;}
    </style>
    <script>
        window.onload = function(){
            var aBtn=document.getElementsByTagName('input');
            var aDiv = document.getElementsByTagName('div');
            for(var i=0;i<aBtn.length;i++){
                aBtn[i].num=i;
                aBtn[i].onclick=function(){
                    for(var i=0;i<aBtn.length;i++){
                        aBtn[i].className=' ';
                        aDiv[i].style.display="none";
                    }
                    this.className='on';
                    aDiv[this.num].style.display="block";
                }
            }
        }
    </script>
</head>
<body>
    <input type="button" value="aaa" class="on">
    <input type="button" value="bbb">
    <input type="button" value="ccc">
    <div style='display:block'>1</div>
    <div>2</div>
    <div>3</div>
</body>
</html>
```

#### Program analysis:

1. A faster way to create repeating elements: like this `input:button*3` 
2. When using custom properties, it's best to have a clear design structure.

### 1.15 Data type

#### Demand

1. click button,add the number in two text boxes.

#### Steps

1. When the alert shows "11" ,we know that the program add two string not two number. The variable in JS just like python : The type of it due to how you use it. (Compound data type) So , our input in text box will be regard as string.
2. use `typeof`can detect data type. Two ways to transform:
   1. Display type conversion:`alert(parseInt(ele_t1.value)+parseInt(ele_t2.value));`
   2. Strict display type conversion:`alert(parseInt(ele_t1.value)+number(ele_t2.value));` Nan(Not a number)is a number type. It's not equal to anything, including itself.
   3. Implicit type conversion:'12'+5->'12'+'5';'12'-'5'->12-5

#### Outcome

#### Program analysis:

## Question(x)

1. JS声明变量的时候，虽然用var关键字声明和不用关键字声明，很多时候运行并没有问题，但是这两种方式还是有区别的。可以正常运行的代码并不代表是合适的代码。

```html
// num1为全局变量，num2为window的一个属性
var num1 = 1;
num2 = 2;
// delete num1;  无法删除
// delete num2;  删除
function model(){
var num1 = 1; // 本地变量
num2 = 2;     // window的属性
}
```

2. 同名声明赋值的变量：逐条进行-后者覆盖前者。（同级别覆盖）

```
var a = 1; 
var a = 2;
console.log(a); // 输出结果：2
```

3. `var f = function () {}` 和 `function f () {}`的区别（有 var 就有内存）

```html
var f = function () {console.log("有var")} // 声明函数
function f () {} // 未声明函数
console.log(f); // 输出结果： 有var的f函数
```

## Solution

Last week:

```html
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
                    alert(count);
                }
            }
```

After these weeks of study, I found that most of the mistakes that were difficult to find were in the order (logical structure). So he tried to switch positions:

```html
for(i=0;i<ele_s.length;i++){
                ele_s[i].onclick=function(){
                    var count=0;
                    for(i=0;i<ele_s.length;i++){
                        if(ele_s[i].checked){count++;}
                    }
                    if(count==ele_s.length){ele_p.checked=true;}
                    else{ele_p.checked=false;}
                    alert(count);
//---------------------------------------------------------
                    ele_s[i].checked=true;	//switch
//---------------------------------------------------------
 
                }
```

1. 上周代码发生点击事件时,没有跳出提示框,换位后可以弹出,并且功能达到预期.
2. 推断在` ele_s[i].checked=true;`处跳出循环
3. 更具这周所学:循环总是先一步完成,点击发生后i等于元素个数,则`ele_s[i]`没有被定义,无法找到.此异常会导致循环中断.
4. 修改方法:使用`this` 替代`ele_s[i]`,上文已提到,就不多说了.