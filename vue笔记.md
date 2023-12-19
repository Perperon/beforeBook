#### 一、vue的基本属性使用

##### 1、v-cloak的用法

```html
<!--v-cloak在解析前有这个属性，解析过后属性消失,可配合样式用来做页面加载时延迟乱码-->
<div id ="app">
  <label>{{message}}</label> 
  <label v-cloak>{{message}}</label> 
</div>
<style>
    [v-cloak]{
        display: none; //有这个属性就显示空白
    }
</style>
<script>
    let app = new Vue({
        el: '#app',
        data: {
            message: '测试'
        }
    });
</script>
```

##### 2、v-once的用法

```html
<!--该指令表示元素和组件只渲染一次，后续不会随着数据改变而改变-->
<div id ="app">
  <label>{{message}}</label> 
  <label v-once>{{message}}</label> 
</div>
<script>
    let app = new Vue({
        el: '#app',
        data: {
            message: '测试'
        }
    });
</script>
```

##### 3、v-html的用法

```html
<!--该指令后面往往会跟上一个string类型，并将string的html解析出来并进行渲染-->
<div id ="app">
    <h2 >{{link}}</h2>
    <h2 v-html="link"></h2>
</div>
<script>
    let app = new Vue({
        el: '#app',
        data: {
            link:'<a href="http://www.baidu.com"></a>'
        }
    });
</script>
```

##### 4、v-text的用法

```html
<!--和mustache语法差不多，用于展示用-->
<div id ="app">
    <h2 >{{link}}</h2>
    <h2 v-text="link"></h2>
</div>
<script>
    let app = new Vue({
        el: '#app',
        data: {
            link:'<a href="http://www.baidu.com"></a>'
        }
    });
</script>
```

##### 5、v-pre的用法

```html
<!--不做任何解析，原封不动的展示出来-->
<div id ="app">
    <h2 >{{message}}</h2>
    <h2 v-pre>{{message}}</h2>
</div>
<script>
    let app = new Vue({
        el: '#app',
        data: {
            message:'hello'
        }
    });
</script>
```

