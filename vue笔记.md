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

##### 6、v-bind绑定的用法

###### (1)、语法糖

```html
v-bind:href语法糖:href
```

###### (2)、动态绑定class

I、对象语法

```html
<div id ="app">
    <h2 >{{message}}</h2>
    <!--第一种-->
    <h2 v-bind:class="{active: isActive,line:isLine}">{{message}}</h2>
    <!--第二种-->
    <h2 :class="getClasses()">{{message}}</h2>
</div>
<script>
    let app = new Vue({
        el: '#app',
        data: {
            message: "实验",
            isActive: true,
            isLine: false
        },
        methods:{
            getClasses(){
               return {active: this.isActive,line: this.isLine};
            }
        }
    });
</script>
```

II、数组语法

```html
<div id ="app">
    <h2 >{{message}}</h2>
    <!--第一种-->
    <h2 v-bind:class="[isActive,isLine]">{{message}}</h2>
    <!--第二种-->
    <h2 :class="getClasses()">{{message}}</h2>
</div>
<script>
    let app = new Vue({
        el: '#app',
        data: {
            message: "实验",
            isActive: "open",
            isLine: "close"
        },
        methods:{
            getClasses(){
               return [this.isActive,this.isLine]
            }
        }
    });
</script>
```

###### (3)、动态绑定style

I、对象语法

```html
<div id ="app">
    <h2 >{{message}}</h2>
    <!--第一种-->
    <h2 v-bind:style="{fontSize: finalSize+'px',color: finalColor}">{{message}}</h2>
    <!--第二种-->
    <h2 :style="getStyles()">{{message}}</h2>
</div>
<script>
    let app = new Vue({
        el: '#app',
        data: {
            message: "实验",
            finalSize: 50,
            finalColor: 'blue'
        },
        methods:{
            getStyles(){
               return {active: this.finalSize,line: this.finalColor};
            }
        }
    });
</script>
```

II、数组语法

```html
<div id ="app">
    <h2 >{{message}}</h2>
    <!--第一种-->
    <h2 v-bind:style="[baseStyle,backStyle]">{{message}}</h2>
    <!--第二种-->
    <h2 :style="getStyle()">{{message}}</h2>
</div>
<script>
    let app = new Vue({
        el: '#app',
        data: {
            message: "实验",
            baseStyle: {fontSize: '100px'},
            backStyle: {backgroundColor: 'red'}
        },
        methods:{
            getStyle(){
               return [this.baseStyle,backStyle]
            }
        }
    });
</script>
```

##### 7、计算属性：computed

I、computed属于属性计算,如果多次调用，计算属性只会调用一次

```html
<div id ="app">
    <h2 >{{sum}}</h2>
</div>
<script>
    let app = new Vue({
        el: '#app',
        data: {
            age: 26,
            number: 30
        },
        computed:{
            sum: function(){
                return this.age + this.number;
            }，
            /*sum:{ //计算属性一般没有set方法，属于只读属性，此方式和上面作用一样
             get: function(){
               return this.age + this.number;
               }   
            }*/
        }
    });
</script>
```
