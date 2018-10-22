## 1,网页一打开，要求依次弹出数字1-6，并且每弹出一次，页面就显示出对应的一个标题行（即从h1-h6）。注意，页面中不应该出现h1-h6的标签，而应该是由js写出来的
~~~
// 定时器 setTimeout() setInterval()
// 如果想重复执行=》使用setInterval()
// 用clearTimeout()阻止函数的执行
(function () {
    let i = 1
    let time = setInterval(function () {
        let h = document.createElement(`H${i}`)
        h.innerHTML = `${i}`
        document.body.appendChild(h)
        i++
        if (i > 6) {
            clearTimeout(time)
            return false
        }
    }, 1000)
})()
~~~
## 2,已知a,b为正整数，且为直角边，求斜边长
~~~
let a=5,b=6
// Math.pow(x,y) // x的y次幂（x,y为数字）
// Math.sqrt(x) // x的平方根（x是大于0的数）
console.log(Math.sqrt(Math.pow(a,2)+Math.pow(b,2)))
~~~
## 3,（表达式，运算符）一个小球从空中掉下来，求如下问题：
a)	如果已知小球掉落时高度为1000m，求其触地瞬间的速度；
b)	如果已知小球落地瞬间的速度（1000m/s），求其掉落时的高度）
/*	附自由落体公式：自由落体的速度规律：v=gt，自由落体的位移规律：h=gt2/2。；（其中g是重力加速度，在地球上g≈9.8m/s2；v是速度，h高度，t是时间）*/
~~~
// 高度为H，时间为t，要算速度，v=gt
// H=(1/2)g*Math.pow(t,2)
// t = Math.sqrt(H/(0.5g))
// v = g(Math.sqrt(H/(0.5g)))
console.log(g(Math.sqrt(1000/(0.5g))))
~~~
## 4, 
~~~
let a = {
    name: 'hai',
    age: 234
}
let b = a
console.log(b.age) // 234
b.age = 23
console.log(a.age) // 23
~~~
## 5，画出倒金字塔
~~~
*****
 ***
  *
<style>
ul{
    list-style: none;
    overflow: hidden;
    text-align: center;
}
li{
    display: inline-block;
    width: 20px;
    height: 20px;
}
</style>
<script type="text/javascript">
    let n = 10,
        i = 0
    for (i; i < n; i++) {
        let ul = document.createElement('ul')
        let li = ''
        console.log(i)
        for (let t=0; t < (n - i); t++) {
            li = document.createElement('li')
            li.innerText = '*'
            ul.appendChild(li)
            document.body.appendChild(ul)
        }
    }
</script>
~~~
## 6,（循环，逻辑分析）输入一个小于10的正整数（比如5），输出如下图案：
~~~
333
22
1
22
333
let n = 5
let ul = document.createElement('ul')
let li = ''
for (let i = n; i <= n && i > 0; i--) {
    let txt = ''
    for (let k = i; k > 0; k--) {
        li = document.createElement('li')
        txt += i
        li.innerHTML = txt
    }
    ul.appendChild(li)
}
for (let i = 1; i <= n; ++i) {
    let txt = ''
    let li = ''
    console.log(i)
    for (let k = i; k >0; k--) {
        li = document.createElement('li')
        txt += i
        li.innerHTML = txt
    }
    ul.appendChild(li)
}
document.body.appendChild(ul)
~~~
## 7.（函数）定义一个函数，该函数可以求两个正数的最大公约数。——约数就是能整除一个数的数，最大公约数就是能同时整除这两个数的最大的那个，比如6和8的最大公约数是2， 15和20的最大公约数是5。