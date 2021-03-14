## cheerio 抓取页面模块

> cheerio是jquery核心功能的一个快速灵活而又简洁的实现，主要是为了用在服务器端需要对DOM进行操作的地方

### 简介

```
cheerio是nodejs的抓取页面模块，为服务器特别定制的，快速、灵活、实施的jQuery核心实现。适合各种Web爬虫程序。
```

```
// 安装
npm install cherrio
// 引入
const cheerio = require("cheerio")
```

### API

后面的例子中用到的HTML模板如下：

```
<ul id="fruits">
  <li class="apple">Apple</li>
  <li class="orange">Orange</li>
  <li class="pear">Pear</li>
</ul>
```

#### 1. 解析html（load）

首先你需要先加载你的HTML。jQuery会自动完成这一步，因为jQuery操作的DOM是固定的。但是在使用cheerio时我们要手动加载我们的HTML文档

首选的方式如下：

```
var cheerio = require('cheerio'),
$ = cheerio.load('<ul id = "fruits">...</ul>');
```

其次，直接把HTML字符串作为上下文也是可以的：

```
$ = require('cheerio');
$('ul', '<ul id = "fruits">...</ul>');
```

或者把HTML字符串作为root

```
$ = require('cheerio');
$('li', 'ul', '<ul id = "fruits">...</ul>');
```

如果你需要自定义一些解析选项，你可以多传递一个对象给load方法：

```
$ = cheerio.load('<ul id = "fruits">...</ul>', {
    ignoreWhitespace: true,
    xmlMode: true
});
```

更多的解析选项可以参考[domhandler](https://link.jianshu.com?t=https://github.com/fb55/domhandler)和[parser-options](https://link.jianshu.com?t=https://github.com/fb55/htmlparser2/wiki/Parser-options)

#### 2. 选择器（selectors）

cheerio的选择器几乎和jQuery一模一样，所以语法上十分相像

```
$( selector, [context], [root] )
```

**selector**在**context**的范围内搜索，**context**的范围又包含在**root**的范围内。**selector**和**context**可以是一个字符串，DOM元素，DOM数组或者cheerio实例。**root**一般是一个HTML文档字符串

选择器是文档遍历和操作的起点。如同在jQuery中一样，它是选择元素节点最重要的方法，但是在jQuery中选择器建立在CSS选择器标准库上。cheerio的选择器实现了大部分的方法

```
$('.apple', '#fruits').text()
//=> Apple

$('ul .pear').attr('class')
//=> pear

$('li[class=orange]').html()
//=> <li class = "orange">Orange</li>
```

#### 3. 属性操作（atrributes）

用来获取和更改属性的方法：

**.attr(name, value)**

这个方法用来获取和设置属性。获取第一个符合匹配的元素的属性值。如果某个属性值被设置成null，那么该属性会被移除。你也可以把**map**和**function**作为参数传递进去，就像在jQuery中一样

```
$('ul').attr('id')
//=> fruits

$('.apple').attr('id', 'favorite').html()
//=> <li class = "apple" id = "favorite">Apple</li>
```

> 更多信息请查看 [http://api.jquery.com/attr/](https://link.jianshu.com?t=http://api.jquery.com/attr/)

**.removeAtrr(name)**

移除名为name的属性

```
$('.pear').removeAttr('class').html()
//=> <li>Pear</li>
```

**.hasClass(className)**

检查元素是否含有此类名

```
$('.pear').hasClass('pear')
//=> true

$('apple').hasClass('fruit')
//=> false

$('li').hasClass('pear')
//=> true
```

**.addClass(className)**

添加类名到所有的匹配元素，可以用函数作为参数

```
$('.pear').addClass('fruit').html()
//=> <li class = "pear fruit">Pear</li>

$('.apple').addClass('fruit red').html()
//=> <li class = "apple fruit red">Apple</li>
```

> 参见 [http://api.jquery.com/addClass/](https://link.jianshu.com?t=http://api.jquery.com/addClass/)

**.remoteClass([className])**

移除一个或者多个（空格分隔）的类名，如果className为空，则所有的类名都会被移除，可以传递函数作为参数

```
$('.pear').removeClass('pear').html()
//=> <li class = "">Pear</li>

$('.apple').addClass('red').removeClass().html()
//=> <li class = "">Apple</li>
```

> 参见 [http://api.jquery.com/removeClass/](https://link.jianshu.com?t=http://api.jquery.com/removeClass/)

#### 遍历

**.find(selector)**

在当前元素集合中选择符合选择器规则的元素集合

```
$('#fruits').find('li').length
//=> 3
```

**.parent()**

获取元素集合第一个元素的父元素

```
$('.pear').parent().attr('id')
//=> fruits
```

**.next()**

选择当前元素的下一个兄弟元素

```
$('.apple').next().hasClass('orange')
//=> true
```

**.prev()**

同**.next()**相反

**.siblings()**

获取元素集合中第一个元素的所有兄弟元素，不包含它自己

```
$('.pear').siblings().length
//=> 2
```

**.children( selector )**

**.each( function(index, element) )**

遍历函数返回false即可终止遍历

```
var fruits = [];

$('li').each(function(i, elem) {
  fruits[i] = $(this).text();
});

fruits.join(', ');
//=> Apple, Orange, Pear
```

**.map( function(index, element) )**

```
$('li').map(function(i, el) {
  // this === el
  return $(this).attr('class');
}).get().join(', ');
//=> apple, orange, pear
```

**.filter( selector )**

```
$('li').filter('.orange').attr('class');
//=> orange
```

**.filter( function(index) )**

```
$('li').filter(function(i, el) {
  // this === el
  return $(this).attr('class') === 'orange';
}).attr('class')
//=> orange
```

**.first()**

```
$('#fruits').children().first().text()
//=> Apple
```

**.last()**

```
$('#fruits').children().last().text()
//=> Pear
```

**.eq( i )**

缩小元素集合，可以用负数表示倒数第 i 个元素被保留

```
$('li').eq(0).text()
//=> Apple

$('li').eq(-1).text()
//=> Pear
```

#### 操作DOM

操作DOM结构的方法

**.append( content, [content, ...] )**

**.prepend( content, [content, ...] )**

**.after( content, [content, ...] )**

```
$('.apple').after('<li class = "plum">Plum</li>')
$.html()
//=>  <ul id = "fruits">
//      <li class = "apple">Apple</li>
//      <li class = "plum">Plum</li>
//      <li class = "orange">Orange</li>
//      <li class = "pear">Pear</li>
//    </ul>
```

**.before( content, [content, ...] )**

```
$('.apple').before('<li class = "plum">Plum</li>')
$.html()
//=>  <ul id = "fruits">
//      <li class = "plum">Plum</li>
//      <li class = "apple">Apple</li>
//      <li class = "orange">Orange</li>
//      <li class = "pear">Pear</li>
//    </ul>
```

**.remove( [selector] )**

```
$('.pear').remove()
$.html()
//=>  <ul id = "fruits">
//      <li class = "apple">Apple</li>
//      <li class = "orange">Orange</li>
//    </ul>
```

**.replaceWith( content )**

```
var plum = $('<li class = "plum">Plum</li>')
$('.pear').replaceWith(plum)
$.html()
//=> <ul id = "fruits">
//     <li class = "apple">Apple</li>
//     <li class = "orange">Orange</li>
//     <li class = "plum">Plum</li>
//   </ul>
```

**.empty()**

```
$('ul').empty()
$.html()
//=>  <ul id = "fruits"></ul>
```

**.html( [htmlString] )**

```
$('.orange').html()
//=> Orange

$('#fruits').html('<li class = "mango">Mango</li>').html()
//=> <li class="mango">Mango</li>
```

**.text( [textString] )**

```
$('.orange').text()
//=> Orange

$('ul').text()
//=>  Apple
//    Orange
//    Pear
```

#### 解析和渲染

```
$.html()
//=>  <ul id = "fruits">
//      <li class = "apple">Apple</li>
//      <li class = "orange">Orange</li>
//      <li class = "pear">Pear</li>
//    </ul>
```

输出包含自己在内的HTML（outer HTML）

```
$.html('.pear')
//=> <li class = "pear">Pear</li>
```

#### 杂项

**.toArray()**

```
$('li').toArray()
//=> [ {...}, {...}, {...} ]
```

**.clone()**

```
var moreFruit = $('#fruits').clone()
```

#### 常用工具

**$.root()**

```
$.root().append('<ul id="vegetables"></ul>').html();
//=> <ul id="fruits">...</ul><ul id="vegetables"></ul>
```

**$.contains( container, contained )**