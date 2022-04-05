# 滑动插件 - jquery.scrollTo

## 一、简介

​	`Jquery.scrollTo`是一款基于Jquery的可定制化的页面滑动插件。



## 二、应用场景

1. **页面内跳转菜单**，实现类似HTML锚点链接的效果；
2. **滑动到指定区域**。



## 三、基本使用

### 1. 下载

#### （1）bower

```shell
bower install jquery.scrollTo
```

#### （2）npm

```shell
npm install jquery.scrollto
```

#### （3）composer

```shell
php composer.phar require --prefer-dist flesler/jquery.scrollto "*"
```

#### （4）直接引入js

```html
<script src="https://cdnjs.cloudflare.com/ajax/libs/jquery-scrollTo/2.1.3/jquery.scrollTo.min.js"></script>
```

### 2. 使用

```html
<!-- 引入js -->
<script type="text/javascript" src="https://code.jquery.com/jquery-1.11.0.js"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/jquery-scrollTo/2.1.3/jquery.scrollTo.min.js"></script>

<!-- 定义可滑动区域及元素 -->
<div id="content" style="width: 100%; height: 100vh; overflow-y: auto;">
    <span>可滑动区域</span>
    <div id="id1" style="height: 500px;">id1</div>
    <div id="id2" style="height: 500px;">id2</div>
</div>
<button type="button" onclick="doAction()">滑动到id1</button>

<!-- 使用 -->
<script>
    function doAction() {
        // 使用scrollTo方法，2s滑动到id2的位置
    	$('#content').scrollTo('#id1', 2000)
    }
</script>
```

>参数解析：
>
>```js
>$('可滑动区域的元素').scrollTo(
>	'滑动至指定的元素',
>    '持续时间'
>)
>```



## 四、扩展参数

### 1. 公式

```js
$(element).scrollTo(target[,duration][,settings]);
```

> element：可滑动区域的元素
>
> target：滑动目标
>
> duration：滑动持续时间
>
> settings：扩展配置，详见[官方文档](https://github.com/flesler/jquery.scrollTo#usage)

### 2. element

​	选择可以进行滑动的元素，如'#content'。

### 3. target

1. **元素选择器**(以下任一种方式)：

   `'#content'` 或 `$('#content')` 或 `document.getElementById('content')`

2. **指定位移**(y轴)：

   - **纯数字，如100**：移动到距离element顶部100的位置；
   - **"100px"**：移动到距离element顶部100的位置；
   - **"50%"**：移动到element 50%的位置；
   - **"+=10px"**：基于当前位置，增加滑动的步长。

### 4. duration/settings

	1. 第二个参数为 `数字` 时，表示：滑动持续多长的时间。
 	2. 第二个参数为 `对象` 时，表示：增加配置。
     - **axis**：触发方向，默认xy，可以为x、y、xy；
     - **interrupt**：用户中止滑动，通过鼠标滚轴等方式中止当前的滑动动画，默认false；
     - **queue**：滑动动画队列，按顺序执行滑动的指令；
     - **onAfter(target, settings)**：滑动完成时触发的事件；
     - 其它配置参数，详见[官方文档](https://github.com/flesler/jquery.scrollTo#usage)。



## 五、Demo案例

> 完整Demo地址：

### 1. 移动指定的距离

![demo1](https://s3.bmp.ovh/imgs/2022/04/05/5e55c02d72e1db05.gif)

```js
// 跳转方法 - 指定位移
function doAction(type) {
    switch (type) {
        // 跳转到800px
        case '800px':
            $('.content').scrollTo('800px')
            // $('.content').scrollTo(800)
            break
        // 相对步长+=100p
        case '+=100px':
            $('.content').scrollTo('+=100px')
            break
        // 跳转到50%
        case '50%':
            $('.content').scrollTo('50%')
            break;
        // 滑到底部
        case 'bottom':
            $('.content').scrollTo('max')
            break
    }
}
```

### 2. 移动到指定的元素

![demo2](https://s3.bmp.ovh/imgs/2022/04/05/7f480fb7539968bd.gif)

```js
// 跳转方法 - 指定元素
function doAction2(id) {
    $('.content').scrollTo(id)
    // $('.content').scrollTo(id, 1000) // 设置滑动的持续时间
}
```

### 3. 设置滑动参数及事件

![demo3](https://s3.bmp.ovh/imgs/2022/04/05/af4ff086d0f8b00c.gif)

```js
// 跳转方法 - 滑动参数及事件
function doAction4() {
    // 参数
    var duration = $('#duration').val()
    var axis = $('#axis').val()
    var interrupt = $('#interrupt').prop('checked')
    var offset = $('#offset').val()
    var queue = $('#queue').prop('checked')
    var onAfter = $('#onAfter').prop('checked')
    if (onAfter) {
        onAfter = function (target, settings) {
            console.log(target);
            console.log(settings);
            alert('滑动结束：' + target[0].id)
        }
    }
    // 元素
    var id = '#blue'
    if (axis == 'x') {
        id = '#blue-right'
    }
    // 跳转
    $('.content').scrollTo(id, {
        duration: parseInt(duration),
        axis: axis,
        interrupt: interrupt,
        offset: offset,
        onAfter: onAfter
    })
}
```



## 六、参考文档

- **Jquery.scrollTo**：https://github.com/flesler/jquery.scrollTo



![公众号二维码](https://s3.bmp.ovh/imgs/2022/04/05/b28ba60b71730f54.png)