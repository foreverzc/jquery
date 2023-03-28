# jQuery

## jQuery的基本使用

+ 等着页面加载完毕再去执行js代码的两种方式

  ``` js
         //1.等着页面DOM加载完毕再去执行js代码
         // $(document).ready(() => {
          //     $('div').hide()
          // })
        2.等着页面DOM加载完毕再去执行js代码
          $(function () {
              $('div').hide()
          })
  ```

+ ==相当于 原生js 中的 DOMContentLoaded 事件  在原生js中 事件流里面==



## jquery 的顶级对象 $

1. $是jQuery 的别称，在代码中可以使用 jquery 代替 ,但一般为了方便 通常直接食用

``` js
        jQuery(function () {
            $('div').hide()
        })
```

2. ==$ 同时也是jQuery 的 顶级对象==



### jQuery对象和DOM对象

+ jQuery 对象，用jQuery 获取过来的就是jQUery 对象，
  + 本质通过$吧DOM元素进行了包装 产生的对象（伪数组形式存储）
+ DOM 对象，用原生js 获取过来的 DOM对象

``` js
        // DOM 对象，用原生js 获取过来的 DOM对象
        let myDiv = document.querySelector('div');
        console.dir(myDiv)
        // 2jQuery 对象，用jQuery 获取过来的就是jQUery 对象，本质通过$吧DOM元素进行了包装 产生的对象（伪数组形式存储）
        $('div'); //$('div') 是一个jQuery对象
        console.dir($('div'))
        // 3.jQuery 对象只能使用jQuery 方法 DOM对象则使用原生的JavaScript 属性和方法
        myDiv.style.display = 'none'
        $('div').style.display = 'none'  //不可以使用 
```



### jQuery对象和DOM对象 转换

1. DOM对象转换为jQuery:

语法：

``` js
$(DOM 对象)
```



``` js
        //1.DOM对象转换为jQuery 对象
        //(1)我们直接获取视频，得到的就是jQuery对象
        $('video');
        //(2)我们已经使用原生js 获取过来DOM对象、
        var mov = document.querySelector('video');
        $(mov).play;//jQuery里面没有paly 方法
```

2. jQuery对象转换为DOM对象

语法：

``` js
$('div')[index]  //index是索引号
$('div').get(index) //index是索引号
```

``` js
        // 2.jQuery对象转换为DOM对象
        mov.play();
        $('vedio')[0].paly()//转化为DOM对象
        $('vedio').get[0].paly()//转换为DOM对象
```



## jQuery 常用API

### jQuery 基础选择器

统一语法格式

``` js
$('选择器')// 里面直接写css选择器即可 但是要加 引号
```



| 名称       | 用法          | 描述                                          |
| ---------- | ------------- | --------------------------------------------- |
| ID选择器   | $('#id')      | 获取指定ID的元素                              |
| 全选选择器 | $('*')        | 匹配所有元素                                  |
| 类选择器   | $('.class')   | 获取同一类的class元素                         |
| 标签选择器 | $('div')      | 获取同一类标签的所有元素                      |
| 并集选择器 | $('div,p,li') | 获取多个元素                                  |
| 交集选择器 | $(li.current) | 交集元素                                      |
| 子代选择器 | $('ul>li')    | 使用>号 获取亲儿子层级的元素                  |
| 后代选择器 | $('ul li')    | 使用空格 代表后代选择器，获取ul下的所有li元素 |

### jQuery 设置样式

语法：

``` js
$('div').css('属性','值')
```



###  隐式迭代（重要）

遍历内部DOM元素，（伪数组形式存储）的过程叫做隐式迭代

简单理解：==给匹配到所有元素进行循环遍历，执行相应的方法，而不用我们再进行循环==，简化我们的操作

``` js
    <div>惊喜不，意外不</div>
    <div>惊喜不，意外不</div>
    <div>惊喜不，意外不</div>
    <div>惊喜不，意外不</div>
    <ul>
        <li>相同的操作</li>
        <li>相同的操作</li>
        <li>相同的操作</li>
        <li>相同的操作</li>
    </ul>
    <script>
        //1.获取四个div元素
        console.log($("div"));

        //2.给四个div设置背景颜色为粉色  jquery 对象不能使用style
        $("div").css("background", 'pink');

        //3.隐式迭代就是把匹配所有元素内部进行遍历循环，给每一个元素都添加css这个方法
        $("ul li").css("color", "red")
```



### jQuery 筛选选择器

| 语法       | 用法           | 描述                                                    |
| ---------- | -------------- | ------------------------------------------------------- |
| :first     | $('li:first')  | 获取第一个元素                                          |
| :last      | $('li:first')  | 获取最后一个元素                                        |
| :eq(index) | $('li:eq(2))') | 获取到li元素中，选择索引号为2的元素，索引号index从0开始 |
| :odd       | $('li:odd')    | 获取到li元素中，选择索引号为奇数的元素                  |
| :even      | $('li:even')   | 获取到l元素中，选择索引号为偶数的 元素                  |

### jQuery 筛选方法（重点）

+ 下面的相当于 方法 函数 不要忘加（）

| 语法                 | 用法                            | 说明                                               |
| -------------------- | ------------------------------- | -------------------------------------------------- |
| parent（）           | $('li').parent();               | 查找父级                                           |
| children（selector） | $('ul').children('li');         | 相当于$('ul>li')，最近一级（亲儿子）               |
| find（selector）     | $('ul').find('li');             | 相当于$('ul li')，后代选择器                       |
| siblings（selector） | $('.first').sibling('li');      | 查找所有兄弟节点，不包括自己                       |
| nextAll（selector）  | $('.first').nextAll();          | 查找当前元素之后所有的同辈元素                     |
| prevtALl（selector） | $('.last').prevAll();           | 查找当前元素之前所有的同辈元素                     |
| hasClass（selector） | $('div').hasClass('protected'); | 检查当前的元素是否含有某个特定的类，如果有返回true |
| eq（index）          | $('li').eq(2);                  | 相当于$('li:eq(2)')，index从0开始                  |
|                      | $('li').parent(0)               | 祖先从0开始计算 0 是亲爹 也可以写指定的选择器      |

### jQuery 排他思想

+ 当前元素设置样式，其余兄弟元素清除样式

``` js
 <button>快速</button>
    <button>快速</button>
    <button>快速</button>
    <button>快速</button>
    <button>快速</button>
    <button>快速</button>
    <button>快速</button>
    <script>
        //jquery 里面的 排他思想
        $(function () {
            // 1.隐式迭代  给所有的按扭都绑定了 点击事件
            $("button").click(function () {
                //2.当前的元素变化背景颜色
                $(this).css("background", "pink")
                //3.其余的兄弟去掉背景颜色  隐式迭代
                $(this).siblings("button").css("background", "");
            })
        })
    </script>
```





## jQuery 操作样式

### jQuery 操作样式 css 方法

1. 参数只写属性名，则是返回属性值

   ``` js
   $(this).css('color');
   ```

2. 参数是==属性名，属性值，逗号分隔== 是设置一组样式，属性必须加分号，值如果是数字可以不用跟单位和引号

   ``` js
   $(this).css('color','red');
   ```

   

3. 参数可以是对象形式，方便设置多组样式，属性名和属性值，用冒号隔开，属性不用加引号

   ``` js
             //修改多个样式
               $('div').css({
                   // 必须加逗号
                   width: 400,
                   // backgroundColor: 'red'
                   height: 400,
                   backgroundColor: 'red',
                   //如果是复合属性则必须采取驼峰命名法，如果值不是数字，则需要加 引号
               })
   ```

   ### jQuery 操作样式操作类

   1. 添加类

   ``` js
   $('div').addClass('current');
   ```

   2. 删除类 removeClass()

   ``` js
   $('div').removeClass('current');
   ```

          3. 切换类

   ``` js
   $('div').toggleClass('current');
   ```

例如

``` html 
    <style>
        .box {
            width: 150px;
            height: 150px;
            background-color: pink;
            margin: 100px auto;
            transition: all 0.5s;
        }

        .current {
            background-color: red;
            transform: rotate(360deg);
        }
    </style>
    <script src="jquery.min.js"></script>
</head>

<body>
    <div class="box"></div>
    <script>
        // 1.添加类
        $('div').click(function () {
            // $(this).addClass('current')
        });
        //2.删除类 removeClass()
        $('div').click(function () {
            // $(this).removeClass('box')
        })
        //3.切换类
        $('div').click(function () {
            $(this).toggleClass('current')
        })
    </script>
</body>
```



## jQuery 效果

### 显示隐藏效果

**显示隐藏切换**

语法：

``` js
show({speed,[easing],[fn]})

hide({speed,[easing],[fn]})

toggle({speed,[easing],[fn]})
```

+ 参数可以都省略 无动画直接显示
+ speed ：三种预定速度之一的字符串（’show‘，’normal‘， ’fast‘）或表示动画时长的毫秒数值（如：1000）
+ easing：（Optional）用来指定切换效果，默认是‘swing’ ，可用参数  ‘linear’
+ fn：回调函数，在动画完成执行的函数，每个元素执行一次

例子

``` js
<style>
        div {
            width: 150px;
            height: 300px;
            background-color: pink;
        }
    </style>

    <script src="jquery.min.js"></script>
</head>

<body>
    <button>显示</button>
    <button>隐藏</button>
    <button>切换</button>
    <div></div>
    <script>
        $(function () {
            $('button').eq(1).click(function () {
                // hide([speed,[easing]],[fn]) 
                //speed: 三种预定速度之一的字符串 ('show','normal',or 'fast')或表示动画时长的毫秒数如(1000)
                //easing:(Optional)用来切换效果，默认是'swing',可用参数'linear'
                //fn：回顾函数，在动画完成时执行的函数，每个元素执行一次
                $('div').hide(1000, function () {
                    alert(1)
                });
            })
            $('button').eq(0).click(function () {
                $('div').show(1000, function () {
                });
            })
            $('button').eq(2).click(function () {
                $('div').toggle(1000)
            })
            //一般情况下 我们都不加参数直接 显示隐藏就可以了
        })
    </script>
```

### 滑动效果

``` js
slideDown([speed],[easing],[fn])
slideUp([speed],[easing],[fn])
slideToggle([speed],[easing],[fn])
```

+ 参数可以都省略 无动画直接显示
+ speed ：三种预定速度之一的字符串（’show‘，’normal‘， ’fast‘）或表示动画时长的毫秒数值（如：1000）
+ easing：（Optional）用来指定切换效果，默认是‘swing’ ，可用参数  ‘linear’
+ fn：回调函数，在动画完成执行的函数，每个元素执行一次

``` js
<style>
        div {
            width: 150px;
            height: 300px;
            background-color: pink;
            display: none;
        }
    </style>

    <script src="jquery.min.js"></script>
</head>

<body>
    <button>下拉滑动</button>
    <button>上拉滑动</button>
    <button>切换滑动</button>
    <div></div>
    <script>
        $(function () {
            $('button').eq(0).click(function () {
                //下滑动slideDown(speed,[easing],[fn]) 
                $('div').slideDown(500);
            })
            $('button').eq(1).click(function () {
                //上滑动slideUp()
                $('div').slideUp(1000);
            })
            $('button').eq(2).click(function () {
                //下滑动slideToggle()
                $('div').slideToggle(3000);
            })
        })
    </script>
```



### 切换事件

``` js
hover([over,]out)
```

+ over:鼠标经过这个元素就要触发这个函数（相当于mouseenter）

+ out：鼠标离开的时候触发（相当于mouseleave）

+ ``` js
   $(".nav>li").hover(function () {
                  $(this).children("ul").slideDown(200);
              }, function () {
                  $(this).children("ul").slideUp(200);
              })
    
              // 2. 事件切换 hover  如果只写一个函数，那么鼠标经过和鼠标离开都会触发这个函数
              $(".nav>li").hover(function () {
                  $(this).children("ul").slideToggle();
              });
          })
  ```



### 动画队列机器停止排队方法（重要）

**1 动画或效果队列**

动画效果一旦触发就会执行，如果多次触发，就造成多个动画或者效果排队执行

+ ==最好动画都加上 stop（）==

**2 停止排队**

``` js
stop()
```

+ ==stop() 方法用于停止动画或效果==
+ 注意：stop（）写到动画或者效果的前面。相当于停止结束上一次的动画

``` js
            $(".nav>li").hover(function () {
                $(this).children("ul").stop().slideToggle();
            });
```

### 淡入淡出效果

``` js
fadeIn([speed,][easing],[fn])

fadeOut([speed,][easing],[fn])

fadeToggle([speed,][easing],[fn])

```

+ 参数可以都省略 无动画直接显示
+ speed ：三种预定速度之一的字符串（’show‘，’normal‘， ’fast‘）或表示动画时长的毫秒数值（如：1000）
+ easing：（Optional）用来指定切换效果，默认是‘swing’ ，可用参数  ‘linear’
+ fn：回调函数，在动画完成执行的函数，每个元素执行一次

``` js
fadeTo(speed，opacity[easing],[fn])
```

+ opacity==透明度==必须写==，取值0-1之间==。
+ speed ：三种预定速度之一的字符串（’show‘，’normal‘， ’fast‘）或表示动画时长的毫秒数值（如：1000） ==必须写==



### 自定义动画 animate

语法

``` js
animate(params,[speed],[easing],[fn])
$('div').animate({
  left:500,
  top:300,
  opacity:.4
},500)
```



参数

+ params ：==想要更改的样式属性，以对象形式传递，必须写==。属性名可以不带引号，如果是复合属性则需要采取驼峰命名法，==其余参数都可省略==
+ speed ：三种预定速度之一的字符串（’show‘，’normal‘， ’fast‘）或表示动画时长的毫秒数值（如：1000）
+ easing：（Optional）用来指定切换效果，默认是‘swing’ ，可用参数  ‘linear’
+ fn：回调函数，在动画完成执行的函数，每个元素执行一次



























































































