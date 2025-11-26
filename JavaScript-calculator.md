# 第一次完整写出前端项目（web计算器）
## HTML代码
```HTML
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>calculater</title>
    <link rel="stylesheet" href="cal.css">
</head>
<body>
    <div class="calculater">
        <div class="screen">
            <div class="pre"></div>
            <div class="current"></div>
        </div>
        <div class="buttons">
            <button class="function btn-del">X</button>
            <button class="function">AC</button>
            <button class="function">*</button>
            <button>7</button>
            <button>8</button>
            <button>9</button>
            <button class="function">÷</button>
            <button>4</button>
            <button>5</button>
            <button>6</button>
            <button class="function">+</button>
            <button>1</button>
            <button>2</button>
            <button>3</button>
            <button class="function">-</button>
            <button>0</button>
            <button class="btn-equal">=</button>
        </div>
    </div>
  <script src="cal.js"></script>  
</body>
</html>
```


## CSS代码
```CSS
body {
    background-color:#eee;
    margin: 0;
    height: 100vh;
    display: flex;
    justify-content: center;
    align-items: center;
}
* {
    box-sizing: border-box;
    padding: 0;
    margin: 0;
}
.calculater {
    width: 400px;
    height: 800px;
    background-color: black;
    border-radius: 50px;
}
.buttons {
    display: grid;
    grid-template-columns: repeat(4,1fr);
    grid-template-rows: repeat(5,1fr);
    gap: 10px;
}
.screen {
    height: 240px;
    display: flex;
    font-size: 40px;
    color: #fff;
    flex-direction: column;
    align-items: flex-end;
    padding-right: 10px;
    padding-top: 10px;
}
.current {
    font-size: 60px;
}
.buttons button {
    height: 70px;
    width: 70px;
    background-color: #333;
    border: none;
    border-radius: 50%;
    font-size: 40px;
    color: #fff;
    margin: 10px;
}
 .buttons .btn-del {
    grid-column-start: 1;
    grid-column-end: 3;
    width: 180px;
    border-radius: 20px;
}
.buttons .btn-equal {
    grid-column-start: 2;
    grid-column-end: 5;
    width:270px;
    border-radius: 20px;
}
.buttons .function {
    background-color: rgb(228, 174, 40);
}
.buttons button:active {
    filter: brightness(150%);
}
```


## JavaScript代码
```JavaScript
// 获取信息
const currrentScreen = document.querySelector('.current');
const previousScreen = document.querySelector('.pre');
const buttons = document.querySelectorAll('button');
 
// 用来记录当前输入的数字
let currentNum = '';
// 用来记录当前上一个的数字
let previousNum = '';
let operation = null;

//定义屏幕更新函数 
function updateDisplay(){
    currrentScreen.innerText = currentNum;
    if(operation != null)
    {
        previousScreen.innerText = previousNum + '' + operation + currentNum;
    }else
    {
        previousScreen.innerText = previousNum;
    }
}

// 定义核心计算函数
function calculate()
{
    let result;
    const pre = parseFloat(previousNum);
    const cur = parseFloat(currentNum);
    
    if(isNaN(pre) || isNaN(cur)) return;
    
    switch(operation)
    {
        case '+':
            result = pre + cur;
            break;
        case '-':
            result = pre - cur;
            break;
        case '*':
            result = pre * cur;
            break;
        case '÷':
            result = pre / cur;
            break;
    }

    currentNum = result;
    operation = null;
    previousNum = '';
}

// 为所有按钮添加点击事件
buttons.forEach(button => {
    button.addEventListener('click',() => {
        let val = button.innerText;

        if(val === 'AC')
        {
            previousNum = '';
            currentNum = '';
            operation = null;
            updateDisplay();
        }
        else if(val === 'X')
        {
            currentNum = currentNum.toString().slice(0,-1);
            updateDisplay();
        }
        else if(val === '=')
        {
            calculate();
            updateDisplay();
        }
        else if(['+','-','*','÷'].includes(val))
        {
            if(currentNum === '') return;

            if(previousNum != '')
            {
                calculate();
            }
            operation = val;
            previousNum = currentNum;
            currentNum = '';
            updateDisplay();
        }
        else
        {
             if (val === '0' && currentNum === '0') return;
            
            // 拼接字符串：把新点击的数字加到后面 (比如 "1" + "2" = "12")
            currentNum = currentNum.toString() + val.toString();
            updateDisplay();
        }
    })
})
```

- 实际体验下来不足的地方
  - 做除法时，如果小数点太多，计算结果会超出屏幕
  - currentScreen并不能实时显示计算结果，显示的是currentNum
  - 计算完一个结果，继续点数字，并不能开启下一段计算
