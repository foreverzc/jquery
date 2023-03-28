# jQuery 属性操作

## 设置或获取元素

+ 所有元素固有属性就是元素本身自带的属性，比如<a> 里面的 href 等

### 获取属性值固有属性值 prop（）

语法:

``` js
prop('属性')
```

``` js
            // 获取属性
            console.log($('a').prop('href'));
            // 修改属性
            $('a').prop('title', '我们都挺好')
```

### 设置或获取元素自定义属性值attr（)

语法

**获取属性语法**

``` js
attr('属性') //类似原生getAttribute
```

**设置属性语法**

``` js
attr('属性','属性值')
```



``` js
    				<div index='1' data-index='2'>我是div</div>
						//2.元素的自定义属性 我们通过attr()  类似原生setAttribute()
            // 获取属性
            console.log($('div').attr('index'));//1
            // 修改属性
            $('div').attr('index', 4)//元素显示  index =  4
            console.log($('div').attr('data-index'));

```

### 数据缓存 data（）

+ data（）方法可以在指定的元素上存取数据，并不会修改DOM元素结构，一旦页面刷新，之前存放的数据都将被移除

``` js
						    <span>123</span>
            //3.数据缓存data()这个里面的 数据是存放在元素内存里面
            $('span').data('uname', 'andy')
            console.log($('span').data('uname'));
            //这个方法获取data-index h5 自定义属性  第一个不用写 data-  而且返回的是数字型
            console.log($('div').data('index'));
```


## jQuery 内容文本值

### 普通元素内容 html（） （相当于原生innerHTML）

``` js
html（） //获取元素内容
html（'内容'） //设置元素内容

console.log($('div').html());
$('div').html('123')
```

### 普通元素文本内容text（） （相当于原生innerText）

``` js
console.log($('div').text());
$('div').text('123');//把所有div里面的 文本内容改成123
```

### 获取设置表单值 val（） (相当于原生中的 value)

``` js
//3.获取设置表单值 val()
console.log($('input').val());
$('input').val('123')
```



## jQuery 元素操作

### 遍历元素

jQuery 隐式迭代是对同一类元素做了 同样的操作，如果想要给同一类元素做不同的操作，就需要用到遍历

语法1：

``` js
$('div').each(function(index,domEle){xxx;})
```

1. each()方法遍历匹配每一个元素，==主要用DOM处理==，each每一个
2. 里面的回调函数有2个参数， index 是每个元素的 索引号，demEle是每个DOM元素对象，不是jquery对象

语法2：

``` js
$.each(object,function(index,element){xxx;})
```

1. $.each() 方法 用于 遍历任何对象， 主要用于数据处理 ，比如 数组，对象
2. 里面的函数 有两个参数  index 是每个元素的 索引号，element 遍历内容



### 创建元素

语法：

``` js
$('<li></li>')
```

### 添加元素

#### 内部添加

语法：

``` js
element.append('内容')
```

==把内容放到匹配元素内部最后面==， 类似原生appendChild。



``` js
element.prepend('内容')
```

==内部添加，并且放到内容最前面==

#### 外部添加

``` js
element.after('内容')// 把内容放到目标元素后面
element.before('内容')// 把内容放到目标元素前面
```

+ 内部添加元素，生成之后 是 父子关系
+ 外部添加元素，生成之后 是 兄弟关系

### 删除元素

``` js
element.remove() //删除匹配的元素本身

element.empty() //删除匹配的元素集合中所有的子节点

element.html('') //清空匹配的元素内容
```





## jQuery 尺寸

==方法：==

| 语法                                 | 用法                                                |
| ------------------------------------ | --------------------------------------------------- |
| width（）/ height()                  | 取得匹配元素宽度和高度值，只算width/ height         |
| innerWidth / innerHeight             | 取得匹配元素宽度和高度值 包含padding                |
| outerWidth / outerHeight             | 取得匹配元素宽度和高度值，包含padding、border       |
| outerWidth(true) / outerHeight(true) | 取得匹配元素宽度和高度值包含padding、border、margin |

+ 以上参数为空，则是获取相应值，返回的是数字型。
+ 如果参数为数字，则是修改相应值
+ 参数可以不必写单位