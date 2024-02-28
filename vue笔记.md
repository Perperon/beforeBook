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

##### 6、v-bind的用法

###### (1)、语法糖

```html
v-bind:href  语法糖:href
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
            },
            /*sum:{ //计算属性一般没有set方法，属于只读属性，此方式和上面作用一样
             get: function(){
               return this.age + this.number;
               }   
            }*/
        }
    });
</script>
```

##### 8、let与var的区别

 I、var定义在if或是for块级里面没有作用域；ES5之前if和for没有作用域的概念，只有借助function的作用域来解决；

II、ES6的let在if或是for块级是有作用域；ES5没有闭包，ES6有

##### 9、const的使用

I、const修饰的标识符为常量，不可再次赋值；建议优先使用const,需要改变标识符时才使用let

```js
const a = 20
a =30 //错误：不可以修改再次赋值

const name; //错误：const初始化标识符必须赋值

//常量的含义是指向的对象不能修改，但可以改变对象内部的属性
const obj ={
    name: 'why',
    age: 18
}
obj.name = 'kobi';
obj.age = 52;
```

##### 10、v-on的用法

###### (1)、语法糖

```
v-on:click  语法糖：@click
```

###### (2)、基本使用

```html
<div id ="app">
    <!--用于属性-->
    <button v-click:click="counter++">{{message}}</button>
    <!--用于方法-->
    <button @click="intcrement()">{{message}}</button>
</div>
<script>
    let app = new Vue({
        el: '#app',
        data: {
            counter: 0          
        },
        methods:{
            intcrement(){
               return counter++;
            }
        }
    });
</script>
```

###### (3)、参数传递问题

```html
<div id ="app">
    <!--无参传递-->
    <button @click="intcrement">{{message}}</button>
    <!--有参传递-->
    <button @click="intcrementOne(123,'abc')">{{message}}</button>
    <!--获取event对象-->
    <button @click="intcrementTwo('abc',$event)">{{message}}</button>
</div>
<script>
    let app = new Vue({
        el: '#app',
        data: {
            counter: 0          
        },
        methods:{
            intcrement(){
               return counter++;
            },
            intcrementOne(num,name){
              return console.log(num,name);
            },
            intcrementTwo(name,event){
                return console.log(num,name);
            }
        }
    });
</script>
```

###### (4)、v-on的常用修饰符

I、stop、prevent、once等修饰符的使用

```html
<div id ="app">
    <!--stop可防止按钮冒泡系列错误-->
    <div @click="divClick">
        divClick
        <button @click.stop="btnClick">按钮</button> 
    </div>
    <!--prevent阻止默认事件-->
        <form action="baidu">
            <input type="submit" value="提交" @click.prevent="submitClick">               </input>
        </form>
     <!--监听某个按键的点击-->
     <!--keyup表示抬起按键触发-->
     <input type="text" @keyup="keyup"></input> 
     <!--keydown表示按下按键触发-->
     <input type="text" @keydown="keydown"></input> 
     <!--表示按下enter按键抬起时触发，其他的按键原理一致-->
     <input type="text" @keyup.enter="keyupEnter"></input>

    <!--once只触发一次事件-->
    <button @click.once="btnClickOnce">按钮</button> 
</div>
<script>
    let app = new Vue({
        el: '#app',
        data: {
            counter: 0          
        },
        methods:{
            divClick(){
                console.log('divClick');
            },
            btnClick(){
               console.log('btnClick');
            },
            submitClick(){
               console.log('submitClick');
            },
            keyup(){
               console.log('keyup');
            },
            keydown(){
               console.log('keydown');
            },
            keyupEnter(){
               console.log('keyupEnter');
            },
            btnClickOnce(){
               console.log('btnClickOnce');
            }
        }
    });
</script>
```

##### 11、v-if与v-show的区别

I、v-if是在面板上直接添加或是移除标签，v-show是隐藏并不删除标签

II、v-show的性能更好

##### 12、v-for的用法

###### (1)、遍历数组

```html
<div id ="app">
    <ul>
        <li v-for="item in list">{{item}}</li>
    </ul>
    <ul>
        <li v-for="(item,index) in list">{{item}}.{{index+1}}</li>
    </ul>
</div>
<script>
    let app = new Vue({
        el: '#app',
        data: {
            list: ['why','kobe']         
        }
    });
</script>
```

###### (2)、对象遍历

```html
<div id ="app">
    <ul>
        <li v-for="item in list">{{item}}</li>
    </ul>
    <ul>
        <li v-for="(value,key) in list">{{value}}-{{key}}</li>
    </ul>
     <ul>
        <li v-for="(value,key,index) in list">{{value}}-{{key}}-{{index}}</li>
    </ul>
</div>
<script>
    let app = new Vue({
        el: '#app',
        data: {
            list: {
                name: 'kidi',
                age: 29
            } 
        }
    });
</script>
```

###### (3)、绑定与非绑定key得运用

```html
<div id ="app">
    <!--在集合中间插入元素下标与对应得值不会变-->
    <ul>
        <li v-for="item in list" :key='item'>{{item}}</li>
    </ul>
    <ul>
        <li v-for="(item,index) in list">{{item}}.{{index+1}}</li>
    </ul>
</div>
<script>
    let app = new Vue({
        el: '#app',
        data: {
            list: ['why','kobe']         
        }
    });
</script>
```

##### 13、数组的响应式函数

```html
<!--响应式函数，点击事件可实时同步数组数据显示在界面上-->
<div id ="app">
    <!--在集合中间插入元素下标与对应得值不会变-->
    <ul>
        <li v-for="item in list" :key='item'>{{item}}</li>
    </ul>
    <button @click="btnClick"></button>
</div>
<script>
    let app = new Vue({
        el: '#app',
        data: {
            list: ['why','kobe']         
        },
        methods:{
            btnClick(){
                //添加元素
                this.list.push('aaa');
                //删除元素（删除数组最后的元素）
                this.list.pop();
                //删除元素（删除数组起始的元素）
                this.list.shift();
                //在数组最前面添加元素
                this.list.shift();
                //可用来删除元素、插入元素、替换元素
                //第一个参数是你要操作的起始位置
                //删除元素：第二个参数是用于你要删除几个元素
                this.list.splice(start,number);
                //替换元素：第二个参数是用于你要替换几个元素。后面的参数是你要替换的元素
                this.list.splice(start,3,'a','b','c');
                //添加元素：第二个参数为0
                this.list.splice(start,0,'a','b','c');
                //排序
                this.list.sort();
                //反转
                this.list.reverse();
            }
        }
    });
</script>
```

##### 14、js的高阶函数运用

###### (1)、filter的使用

```js
const nums = [100,12,25,59,78,125,79,85,200];
//filter中的回调函数需要返回一个boolean值
//true:元素加入新的数组
//false:过滤掉该元素
let newnums = nums.filter(function(n){
    return n<100;
});
console.log(newnums);
```

###### (2)、map的使用

```js
const nums = [100,12,25,59,78,125,79,85,200];
//map用于对数组的加工运算，逻辑处理
let newnums = nums.map(function(n){
   return n * 2; 
});
console.log(newnums);
```

###### (3)、reduce的使用

```js
const nums = [100,12,25,59,78,125,79,85,200];
//reduce可用于对数组的汇总运算
//第二参数是初始化值
//preValue是上一次返回的值，n是nums数组里面遍历的元素
let total = nums.reduce(function(preValue,n){
   return preValue + n; 
},0);
console.log(total);

//结合以上函数使用
let totalNum = nums.filter(function(n){
    return n<100;
}).map(function(n){
   return n * 2; 
}).reduce(function(preValue,n){
   return preValue + n; 
},0);
//console.log(totalNum);
//或者
let totalNum = nums.filter(n => n<100).map(n => n*2).reduce((pre,n) => pre + n);
console.log(totalNum);
```

##### 15、v-model双向绑定

###### (1)、基本运用及原理

```html
<div id ="app">
    <input type="text" v-model="message"/> 
    <h2>{{message}}</h2>
    <!--双向绑定原理-->
    <!--valueUpdate没参数而方法有参数，默认参数传递的是event对象，相当于valueUpdate($event)-->
    <input type="text" :value="msg" v-on:input="valueUpdate"/>    
    <input type="text" :value="msg" @input="msg=$event.target.value"/>
</div>
<script>
    let app = new Vue({
        el: '#app',
        data: {
            message: 'hello',
            msg: 'world'
        },
        methods:{
            valueUpdate(event){
                this.msg = event.target.value;
            }
        }
    });
</script>
```

###### (2)、结合radio

```html
<div id ="app">
    <label for="male">
      <input type="radio" v-model="sex" id="male" value="男" name="sex"/>男 
    </label>
    <label for="female">
      <input type="radio" v-model="sex" id="female" value="女" name="sex"/>女
    </label>
    <h2>{{sex}}</h2>        
</div>
<script>
    let app = new Vue({
        el: '#app',
        data: {
            sex: null
        },
        methods:{

        }
    });
</script>
```

###### (3)、结合checkbox

```html
<div id ="app">
    <!--单选运用-->
    <label for="agree">
      <input type="checkbox" v-model="isAgree" id="agree" name="agree"/>男 
    </label>
    <h2>{{isAgree}}</h2> 
    <button :disabled="!isAgree">下一步</button>

    <!--多选运用-->
    <input type="checkbox" v-model="hobbies" name="hobbies" value="篮球"/>篮球
    <input type="checkbox" v-model="hobbies" name="hobbies" value="足球"/>足球
    <input type="checkbox" v-model="hobbies" name="hobbies" value="排球"/>排球
    <input type="checkbox" v-model="hobbies" name="hobbies" value="乒乓球"/>乒乓球
    <h2>{{hobbies}}</h2> 
</div>
<script>
    let app = new Vue({
        el: '#app',
        data: {
            isAgree: false,
            hobbies: []
        }
    });
</script>
```

###### (4)、结合select

```html
<div id ="app">
    <!--单选-->
    <select name="fruit" v-model="fruit">
        <option value="苹果">苹果</option>
        <option value="香蕉">香蕉</option>
        <option value="榴莲">榴莲</option>
        <option value="葡萄">葡萄</option>
    </select>
    <h2>{{fruits}}</h2>

    <!--多选-->
    <select name="fruits" v-model="fruits" multiple>
        <option value="苹果">苹果</option>
        <option value="香蕉">香蕉</option>
        <option value="榴莲">榴莲</option>
        <option value="葡萄">葡萄</option>
    </select>
    <h2>{{fruits}}</h2>
</div>
<script>
    let app = new Vue({
        el: '#app',
        data: {
            fruits: null,
            fruit: null
        },
        methods:{

        }
    });
</script>
```

###### (5)、值绑定

```html
<div id ="app">
    <!--多选-->
    <label v-for="item in hobbies" :for="item">
        <input type="checkbox" v-model="loves" name="loves" :value="item" :id="item">{{item}}
    </label>

    <h2>{{fruits}}</h2>
</div>
<script>
    let app = new Vue({
        el: '#app',
        data: {
            hobbies: ['篮球','足球','羽毛球','排球','铅球'],
            loves: []
        },
        methods:{

        }
    });
</script>
```

###### (6)、常用修饰符的使用

I、lazy可以让数据在失去焦点或回车会更新

II、number让输入的类型必须是数值类型

III、trim去点输入框界面上空格，也自动去掉对象空格

```html
<div id ="app">  
    <!--lazy修饰符-->
    <input type="text" v-model.lazy="message" name="message"/>男       
    <h2>{{message}}</h2>

    <!--number修饰符-->
    <input type="text" v-model.number="age" name="age"/>男       
    <h2>{{age}}</h2>

    <!--trim修饰符-->
    <input type="text" v-model.trim="name" name="name"/>男       
    <h2>{{name}}</h2>
</div>
<script>
    let app = new Vue({
        el: '#app',
        data: {
            message: null,
            age: 0,
            name: '   helloworld'
        },
        methods:{

        }
    });
</script>
```

#### 二、Vue的组件化

##### 1、基本用法

```html
<div id ="app"> 
    <!--使用组件-->
    <my-msg></my-msg>
</div>
<script src="../js/vue.js"></script>
<script>
    //创建组件构造器对象
    const viewVue = Vue.extend({
        template: `
           <div>
              <h2>测试</h2>
              <h2>hello</h2>
              <h2>world</h2>
           </div>`
    });
    //注册组件
    Vue.component('my-msg',viewVue);
    let app = new Vue({
        el: '#app',
        data: {
            message: null
        }      
    });
</script>
```

##### 2、全局组件与局部组件

```html
<div id ="app"> 
    <!--使用组件-->
    <my-msg></my-msg>
</div>
<div id ="app2"> 
    <!--使用组件-->
    <my-msg></my-msg>
</div>
<script src="../js/vue.js"></script>
<script>
    //创建组件构造器对象
    const viewVue = Vue.extend({
        template: `
           <div>
              <h2>测试</h2>
              <h2>hello</h2>
              <h2>world</h2>
           </div>`
    });
    //注册组件(全局组件)
    //Vue.component('my-msg',viewVue);
    let app = new Vue({
        el: '#app',
        data: {
            message: null
        }      
    });

    let app2 = new Vue({
        el: '#app2',
        data: {
            message: null
        },
        components: {//注册组件(局部组件)
            my-msg: viewVue
        }
    });
</script>
```

##### 3、父组件与子组件区分

```html
<div id ="app"> 
    <!--使用组件-->
    <cpn2></cpn2>
</div>
<script src="../js/vue.js"></script>
<script>
    //创建第一个组件构造器对象
    const cpnC1 = Vue.extend({
        template: `
           <div>
              <h2>test</h2>
              <h2>message</h2>
              <h2>这是个测试</h2>
           </div>`
    });
    //创建第二个组件构造器对象
    const cpnC2 = Vue.extend({
        template: `
           <div>
              <h2>测试</h2>
              <h2>hello</h2>
              <h2>world</h2>
              <cpn1></cpn1> 
           </div>`,  
        components:{
            cpn1: cpnC1 //调用第一个组件，cpn1成为子组件
        }
    });

    let app = new Vue({
        el: '#app',
        data: {
            message: null
        },
        components:{
            cpn2: cpnC2 //如果还需单独使用cpn1组件的话，需要在这里注册
        }
    });
</script>
```

##### 4、注册组件语法糖

```html
<div id ="app"> 
    <!--使用组件-->
    <cpn1></cpn1>
    <cpn2></cpn2>
</div>
<script src="../js/vue.js"></script>
<script>
    //注册组件(全局组件)
    Vue.component('cpn1',{
        template: `
           <div>
              <h2>测试</h2>
              <h2>hello</h2>
              <h2>world</h2>
           </div>`
    });
    let app = new Vue({
        el: '#app',
        data: {
            message: null
        },
        components:{
            'cpn2': { //注册组件(局部组件)
                template: `
                   <div>
                      <h2>test</h2>
                      <h2>love</h2>
                      <h2>person</h2>
                   </div>`
            }
        }
    });
</script>
```

##### 5、组件模板抽离

```html
<div id ="app"> 
    <!--使用组件-->
    <cpn1></cpn1>
    <cpn2></cpn2>
</div>
<script src="../js/vue.js"></script>
<!--第一种-->
<script type="text/x-template" id="cpn1">
   <div>
      <h2>测试</h2>
      <h2>hello</h2>
      <h2>world</h2>
   </div>
</script>
<!--第二种-->
<template id="cpn2">
   <div>
      <h2>test</h2>
      <h2>kotlin</h2>
      <h2>java</h2>
   </div>
</template>
<script>
    //注册组件(全局组件)
    Vue.component('cpn1',{
        template: `#cpn1`
    });
    let app = new Vue({
        el: '#app',
        data: {
            message: null
        },
        components:{
            'cpn2': { //注册组件(局部组件)
                template: `#cpn2`
            }
        }
    });
</script>
```

##### 6、组件的data函数

I、组件有自己单独的属性的数据data，而不是放在Vue实例的data中

II、组件的data属性必须是一个函数且需要返回一个对象，对象内部保存着数据

```html
<div id ="app"> 
    <!--组件实例-->
    <cpn></cpn>
    <cpn></cpn>
</div>
<template id="cpn">
   <div>
       <h2>
           当前计数：{{counter}}
       </h2>
       <button @click="incre"></button>
       <button @click="decre"></button>
    </div>
</template>
<script src="../js/vue.js"></script>
<script>
    //注册组件(全局组件)
    Vue.component('cpn',{
        template: `#cpn`,
        data(){ //为何data必须为函数，就是因为组件可在多个地方使用，生成了不同的实例，所以必须用函数
           return{
               counter: 0
           }
        },
        methods:{
            incre(){
                this.counter++
            },
            decre(){
                this.counter--
            }
        }
    });
    let app = new Vue({
        el: '#app',
        data: {
            message: null
        }
    });
</script>
```

##### 7、父子组件通信props与$emit()

###### (1)、通过props向子组件传递数据

```html
<div id ="app"> 
    <!--组件实例-->
    <cpn :cmessage="message" v-bind:clist="list"></cpn>
</div>
<template id="cpn">
   <div>
       <h2>{{cmessage}}</h2>
       <ul>
           <li v-for="item in clist">{{item}}</li>
       </ul>
    </div>
</template>
<script src="../js/vue.js"></script>
<script>
    //注册组件(全局组件)
    Vue.component('cpn',{
        template: `#cpn`,
        props:{
            cmessage:{
                type: String,
                default: ''
            },
            clist:{
                type: Array,
                default(){
                    return{}
                }
            }
        },
        data(){ 
           return{

           }
        }
    });
    let app = new Vue({
        el: '#app',
        data: {
            message: '测试数据传递',
            list: ['苹果','香蕉','橘子']
        }
    });
</script>
```

###### (2)、通过自定义事件向父组件发送消息

```html
<div id ="app"> 
    <cpn @item-click="cpnClick"></cpn>
</div>
<template id="cpn">
   <div>
       <button v-for="item in list" @click="btnClick(item)">
           {{item}}
       </button>
    </div>
</template>
<script src="../js/vue.js"></script>
<script>
    let cpn = {
        template: `#cpn`,
        data(){
            return{
               list:[
                    {id:1,name:'热门商品'},
                    {id:2,name:'其他商品'},
                    {id:3,name:'必须商品'},
                    {id:4,name:'新上商品'}
               ] 
        }
      },
        methods:{
            btnClick(item){
                //发射事件，传消息给父组件:自定义事件
                this.$emit('item-click',item);//子组件中，通过$emit()来触发事件，父组件通过v-on来监听子组件事件
            }
        }
    }
    let app = new Vue({
        el: '#app',
        data: {
            message: '测试数据传递'
        },
        components:{
            cpn
        },
        methods:{
            cpnClick(item){
                console.log('打印',item);
            }
        }
    });
</script>
```

###### (3)、props的驼峰标识

```html
<div id ="app"> 
    <!--props的驼峰标识规则-->
    <cpn :c-message="message" v-bind:c-list="list"></cpn>
</div>
<template id="cpn">
   <div>
       <h2>{{cMessage}}</h2>
       <ul>
           <li v-for="item in cList">{{item}}</li>
       </ul>
    </div>
</template>
<script src="../js/vue.js"></script>
<script>
    //注册组件(全局组件)
    Vue.component('cpn',{
        template: `#cpn`,
        props:{
            cMessage:{
                type: String,
                default: ''
            },
            cList:{
                type: Array,
                default(){
                    return{}
                }
            }
        },
        data(){ 
           return{

           }
        }
    });
    let app = new Vue({
        el: '#app',
        data: {
            message: '测试数据传递',
            list: ['苹果','香蕉','橘子']
        }
    });
</script>
```

###### (4)、双向绑定案例

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>父子组件的双向绑定</title>
</head>
<body>
<div id ="app">
    <cpn v-model="message"></cpn>
    <!--  等同于上面所示  -->
    <cpn :value="message" @input="messageData"></cpn>
</div>
<template id="cpn">
    <div>
        <h2>{{value}}</h2>
        <input type="text" :value="value" @input="updateValue"/>
    </div>
</template>
</body>
<script src="../js/vue.min.js"></script>
<script>
    //注册组件(全局组件)
    Vue.component('cpn',{
        template: `#cpn`,
        props:{
            value:{
                type: String,
                default: ''
            }
        },
        data(){
            return{
            }
        },
        methods: {
            updateValue(event){
                let value = event.target.value;
                this.$emit('input',value);
            }
        }
    });
    let app = new Vue({
        el: '#app',
        data: {
            message: ''
        },
        methods:{
            messageData(value){
                this.message = value;
                console.log(value);
            }
        }
    });
</script>
</html>
```

###### (5)、双向绑定案例-watch监听实现

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>父子组件的双向绑定-watch监听实现</title>
</head>
<body>
<div id ="app">
    <form-input v-model="message"></form-input>
    <!--  等同于上面所示  -->
    <form-input :value="message" @input="messageData" placeholder="这是一个测试" ></form-input>
</div>
<template id="cpn">
    <div>
        <h2>{{value}}</h2>
        <input type="text" :placeholder="placeholder" v-model="value"/>
    </div>
</template>
</body>
<script src="../js/vue.min.js"></script>
<script>
    //注册组件(全局组件)
    Vue.component('form-input',{
        template: `#cpn`,
        props:{
            value:{
                type: String,
                default: ''
            },
            placeholder:{
                type: String,
                default: '请输入信息'
            }
        },
        data(){
            return{
            }
        },
        watch: {
            value(newValue,oldValue){
                this.$emit('input',newValue);
            }
        }
    });
    let app = new Vue({
        el: '#app',
        data: {
            message: ''
        },
        methods:{
            messageData(value){
                this.message = value;
                console.log(value);
            }
        }
    });
</script>
</html>
```

##### 8、父子组件的访问方式

###### (1)、父组件访问子组件$children与$refs.reference

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>父组件访问子组件</title>
</head>
<body>
<div id ="app">
    <cpn></cpn>
    <cpn></cpn>
    <cpn ref="compent"></cpn>
    <button @click="btnClick">测试</button>
</div>
<template id="cpn">
    <div>
        <h2>测试数据传递</h2>
        <button @click="showMessage">按钮</button>
        <input ref="input" :value="value" @input="updateValue">
    </div>
</template>
</body>
<script src="../js/vue.min.js"></script>
<script>
    let app = new Vue({
        el: '#app',
        data: {
            message: '测试数据传递'
        },
        methods:{ //可通过$children与$refs获取组件的属性和方法
            btnClick(){
                /*for(let i of this.$children){//$children返回相同标签的所有数组
                    console.log(i.name);
                    console.log(i.showMessage());
                }*/
                console.log(this.$refs.compent);//通过$refs与ref="xxx"准确定位一个标签
                console.log(this.$refs.compent.name);
                console.log(this.$refs.compent.showMessage());
            }
        },
        components:{
            cpn:{
                template: '#cpn',
                props:{
                    value:{
                        type: String,
                        default() {
                            return '';
                        }
                    }
                },
                data(){
                    return{
                        name: '杜彭'
                    }
                },
                methods:{
                    showMessage(){
                        console.log('测试');
                    },
                    updateValue(value){
                        this.$emit("input",value);
                    }
                },
                mounted(){
                    //console.log(this.$refs.input);
                    console.log(this.$el);
                }
            }
        }
    });
</script>
</html>
```

###### (2)、子组件访问父组件$parent

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>子组件访问父组件</title>
</head>
<body>
<div id ="app">
    <cpn></cpn>
</div>
<template id="cpn">
    <div>
        <button @click="cpnClick">按钮1</button>
        <ccpn></ccpn>
    </div>
</template>
<template id="ccpn">
    <div>
        <h2>测试数据传递</h2>
        <button @click="btnClick">按钮2</button>
    </div>
</template>
</body>
<script src="../js/vue.min.js"></script>
<script>
    let app = new Vue({
        el: '#app',
        data: {
            message: '测试数据传递'
        },
        components:{
            cpn:{
                template: '#cpn',
                data(){
                    return{
                        name: '杜彭'
                    }
                },
                methods: {
                    cpnClick() {
                        console.log(this.$parent);
                        console.log(this.$parent.message);
                    }
                },
                components: {
                    ccpn:{
                        template: '#ccpn',
                        methods:{
                            btnClick(){
                                console.log(this.$parent);
                                console.log(this.$parent.name);//获取父级组件的属性与方法

                                console.log(this.$root); //获取根组件
                                console.log(this.$root.message);
                            }
                        }
                    }
                }
            }
        }
    });
</script>
</html>
```

##### 9、插槽的使用

###### (1)、基本使用

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>slot的使用</title>
</head>
<body>
<div id ="app">
    <cpn></cpn>
    <cpn><label>变体：</label><a href="http://www.baidu.com">百度一下</a></cpn><!--替换默认标签-->
</div>
<template id="cpn">
    <div>
        <h2>测试数据传递</h2>
        <slot><button @click="showMessage">按钮</button></slot><!--插槽slot的作用是自由插入所需增加的标签，使组件复用性更高,可设置默认标签-->
    </div>
</template>
</body>
<script src="../js/vue.min.js"></script>
<script>
    let app = new Vue({
        el: '#app',
        data: {
            message: '测试数据传递'
        },
        methods:{

        },
        components:{
            cpn:{
                template: '#cpn',
                data(){
                    return{
                        name: '杜彭'
                    }
                },
                methods: {
                    showMessage(){
                        console.log("showMessage");
                    }
                }
            }
        }
    });
</script>
</html>
```

###### (2)、具名插槽的使用

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>slot的使用</title>
</head>
<body>
<div id ="app">
    <cpn>
        <span slot="left">这是一asdasd</span>
        <span slot="center">这是一个cesium</span>
        <span slot="center">这是一sdfdsfium</span></cpn>
    <cpn>
        <div slot="left">
        <label>变体：</label>
        <a href="http://www.baidu.com">百度一下</a>
        </div></cpn><!--替换默认标签-->
</div>
<template id="cpn">
    <div>
        <h2>测试数据传递</h2>
        <slot name="left"><span>左边</span></slot><!--插槽slot的作用是自由插入所需增加的标签，使组件复用性更高,可设置默认标签-->
        <slot name="center"><span>中间</span></slot><!--多个插槽的使用-->
        <slot name="right"><span>右边</span></slot>
    </div>
</template>
</body>
<script src="../js/vue.min.js"></script>
<script>
    let app = new Vue({
        el: '#app',
        data: {
            message: '测试数据传递'
        },
        components:{
            cpn:{
                template: '#cpn',
                methods: {
                    showMessage(){
                        console.log("showMessage");
                    }
                }
            }
        }
    });
</script>
</html>
```

###### (3)、作用域插槽

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>slot作用域插槽的使用</title>
</head>
<body>
<div id ="app">
    <cpn></cpn>
    <cpn>
        <template slot-scope="slot">
            <span>{{slot.data.join(' - ')}}</span><!--父组件替换插槽的默认标签，但是数据内容由子组件来提供-->
        </template>
    </cpn>
</div>
<template id="cpn">
    <div>
        <slot :data="languages"><!--:data也可以是其他的名称-->
            <ul>
                <li v-for="item on languages">{{item}}</li>
            </ul>
        </slot>
    </div>
</template>
</body>
<script src="../js/vue.min.js"></script>
<script>
    let app = new Vue({
        el: '#app',
        data: {
            message: ''
        },
        components:{
            cpn:{
                template: '#cpn',
                data(){
                    return{
                        languages: ['java','c++','golang','c#']
                    }
                }
            }
        }
    });
</script>
</html>
```

#### 三、前端模块化

##### 1、CommonJS模块化

```js
//如：nodejs与webpack使用
//CommonJS的导出
module.exports = {
    flag: true,
    test(a,b){
        return a+b;
    }
}

//CommonJS的导入 
let {flag,test} = require('文件路径');
```

##### 2、ES6的模块化

```js
//如：webpack使用，webpack依赖nodejs
let name = 'pengcheng';
let age = 23;
function sum(num1,num2){
   return num1+ num2;
}
if(flag){
    console.log(sum(20,30));
}
//方式一
//可导出类、函数、属性
export class Person{
    run(){
       console.log('ssss'); 
    }
}
//方式二
//导出 
export{
   flag,sum,age
}

//方式三
//默认导出 注意：在同一个模块中只能有一个默认导出
export default function (){
    console.log('saddgfdg'); 
}

//导入
import {flag,sum,age,Person} from "文件路径"
//默认导入 名字自定义命名
import func from '文件路径'
//统一导入
import * as list from '文件路径'
```

##### 3、webpack的使用

I、webpack是一个现代的javascript应用的静态模块打包工具,依赖nodejs

###### (1)、环境搭建安装

I、安装全局webpack

```properties
npm install webpack@3.6.0 -g
```

II、安装局部webpack

```properties
npm install webpack@3.6.0 --save-dev   #--save-dev表示开发时依赖，打包后不需要webpack
```

III、在终端执行webpack命令，使用的是全局安装的webpack；当在package.json中的scripts定义时了webpack命令时，使用的时局部webpack

###### (2)、webpack基本使用

I、utils.js创建

```js
//CommonJs模块化
function add(num1,num2){
    return num1 + num2;
}
function del(num1,num2){
    return num1 - num2;
}
module.exports ={
    add,del
}
```

II、info.js创建

```js
export let name = 'pengcheng';
export function func(num1,num2){
    return num1 * num2;
}
```

III、main.js创建

```js
const {add,del} = require('./utils');
console.log(add(20,30));
console.log(del(20,30));
import {name,func} from './info.js';
console.log(name);
console.log(func(20,30));
```

IIII、index.html创建

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>index</title>
</head>
<body>
    <div id ="app">

    </div>
</body>
<script src="./dist/bundle.js"></script>

</html>
```

IIIII、使用命令编译打包

```properties
webpack ./src/main.js ./dist/bundle.js #将mian.js中的源码、引用以及引用文件的引用一起打包为bundle.js里面
```

###### (3)、进阶：配置文件

I、webpack.config.js配置

```js
//这是nodejs里面的包 需要npm init初始化项目
const path = require('path')
module.exports = {
    //入口
    entry: './src/main.js',
    //出口
    output:{
        path: path.resolve(_dirname,'dist'),//拿到绝对路径
        filename: 'bundle.js'
    }
}
```

II、使用命令编译打包

```properties
webpack
```

III、package.json配置

```json
{
  "name": "demo",
  "version": "1.0.0",
  "main": "main.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1",
     "build": "webpack" //配置编译打包命令，也可写一个配置文件然后引用
  },
  "author": "",
  "license": "ISC",
  "description": ""
}
```

IIII、命令编译打包

```properties
npm run build #代替webpack
```

###### (4)、css文件配置

I、安装css的loader

```properties
npm install --save-dev css-loader   #具体其他类型文件loader安装可去webpack官网文档查看
npm install --save-dev style-loader #style-loader 与 css-loader 一起使用
```

II、配置webpack.config.js文件

```js
module.exports = {
  //加入css配置
  module: {
    rules: [
      {
        test: /\.css$/i,
          //css-loader只负责加载，不负责解析，style-loader负责解析到DOM中 
          //多个loader是从右往左读
        use: ["style-loader", "css-loader"]
      },
    ],
  },
};
```

III、style.css文件创建

```css
body {
  background: green;
}
```

IIII、引入你的css样式文件

```js
import "./style.css";   #然后可用npm run build打包了  其他文件也是类似操作
```

```js
//其他步骤与css文件引入相似
const path = require('path')
module.exports = {

}
```

###### (5)、图片文件配置

I、安装图片的loader

```properties
npm install --save-dev url-loader
```

II、引入文件

```js
import img from './image.png'
```

III、配置webpack.config.js文件

```js
module.exports = {
    //入口
    entry: './src/main.js',
    //出口
    output:{
        path: path.resolve(_dirname,'dist'),//拿到绝对路径
        filename: 'bundle.js',
        publicPath: 'dist/' //打包过后页面能访问到编译后图片，需配置publicPath
    }，
  //加入url配置
  module: {
    rules: [
       {
        test: /\.(png|jpe?g|gif|svg)(\?.*)?$/,
        use:[
          {
            loader: 'url-loader',
            options: {
             //大于limit时，使用file-loader模块进行加载
             //小于limit时，使用base64字符串进行加载
              limit: 10000, 
              name: 'img/[name].[hash:7].[ext]' //给图片配置别名
            }

          }
        ]      
      }
    ]
  }
};
```

###### (6)、ES6转ES5的babel配置

I、安装处理的loader

```properties
npm install --save-dev babel-loader@7 babel-core babel-preset-es2015
```

II、配置webpack.config.js文件

```js
module: {
  rules: [
    {
      test: /\.m?js$/,
      exclude: /(node_modules|bower_components)/,
      use: {
        loader: 'babel-loader',
        options: {
          presets: ['es2015']
        }
      }
    }
  ]
}
```

##### 4、webpack配置Vue

###### (1)、配置环境

I、安装Vue

```properties
npm install --save vue
```

II、导入vue

```js
import Vue from 'vue'
```

III、配置webpack.config.js文件

```js
module.exports = {
   resolve:{
     alias:{ //别名
        ‘vue$’:'vue/dist/vue.esm.js' //默认使用vue.runtime.js,没有编译template的环境，需要重新指定
     }
   }
}
```

###### (2)、vue的template与el的关系

I、template里面定义的页面标签会覆盖el定义的id标签

###### (3)、vue在模块化的使用

I、安装vue的相关loader

```properties
npm install vue-loader vue-template-compiler --save-dev    #14版本以上需要配置插件
```

II、配置webpack.config.js文件

```js
module:{
    rules:[
        {
            test: /\.vue$/,
            use: ['vue-loader']
        }
    ]
}
```

III、创建index.html页面入口

```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8">
    <title>mall-admin-web</title>
  </head>
  <body>
    <div id="app"></div>
  </body>
</html>
```

IIII、创建main.js

```js
import Vue from 'vue'
import App from './App'
new Vue({
  el: '#app',
  template: '<App/>', //组件引用
  components: { App } //App.vue文件实现组件
})
```

IIIII、创建App.vue文件

```vue
<template>
  <div>
    <h2 class="title">{{message}}</h2>
    <button @click="btnClick">
        按钮
    </button>
  </div>
</template>

<script>
  export default {
    name: 'App',
    data(){
        return{
            message: 'hello'
        }
    },
    methods:{
        btnClick(){
            console.log("hello");
        }
    }
  }
</script>

<style>
    .title{
        color: red;
    }
</style>
```

IIIIII、引入省略后缀配置

```js
module.exports = {
   resolve:{
     extensions: ['.js','.css','.vue'] //引用后缀名省略
     alias:{ //别名
        'vue$':'vue/dist/vue.esm.js' //默认使用vue.runtime.js,没有编译template的环境，需要重新指定
     }
   }
}
```

##### 5、webpack的plugin使用

###### (1)、横幅版权plugin

I、配置webpack.config.js配置文件

```js
const webpack = require('webpack')
module.exports = {
  plugins: [
    new webpack.BannerPlugin('最终版权归xxx所有')
  ]
}
```

###### (2)、打包html的plugin

I、安装插件

```properties
npm install html-webpack-plugin --save-dev
```

II、配置webpack.config.js配置文件

```js
const HtmlWebpackPlugin = require('html-webpack-plugin')
module.exports = {
    //入口
    entry: './src/main.js',
    //出口
    output:{
        path: path.resolve(_dirname,'dist'),//拿到绝对路径
        filename: 'bundle.js',
        //publicPath: 'dist/' //使用html-webpack-plugin可注释掉publicPath，html-webpack-plugin会自动创建一个index.html，并引入js
    }，
  plugins: [
    new HtmlWebpackPlugin({
        template: 'index.html' //会找到当前目录下的index.html文件为模板生成自己的index.html
})
  ]
}
```

###### (3)、js压缩的plugin

I、安装插件

```properties
npm install uglifyjs-webpack-plugin@1.1.1 --save-dev
```

II、配置webpack.config.js配置文件

```js
const UglifyjsjsPlugin = require('uglifyjs-webpack-plugin')
module.exports = {
  plugins: [
    new UglifyjsjsPlugin()
  ]
}
```

##### 6、webpack搭建测试服务器

###### (1)、安装测试服务

```properties
npm install webpack-dev-server@2.9.1 --save-dev
```

###### (2)、配置webpack.config.js

```js
module.exports = {
 devServer: {
     contentBase: './dist',
     inline: true, //是否实时监听，
     port: 8011 //指定端口
 }
}
```

###### (3)、配置package.json

```json
{
  "name": "demo",
  "version": "1.0.0",
  "main": "main.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1",
    "build": "webpack", //配置编译打包命令，也可写一个配置文件然后引用
    "dev": "webpack-dev-server --open" //open是启动时打开页面进行预览
  },
  "author": "",
  "license": "ISC",
  "description": ""
}
```

###### (4)、执行启动服务命令

```properties
npm run dev
```

##### 7、webpack配置文件分离

###### (1)、创建三个配置文件

```properties
base.config.js  //基础配置  prod.config.js //发布配置  dev.config.js  //测试配置  //在build文件夹里面创建
```

###### (2)、安装配置文件插件

```properties
npm install webpack-merge --save-dev
```

###### (3)、dev.config.js配置

```js
const baseConfig = require('./base.config')
const webpackMerge = require('webpack-merge')
module.exports =webpackMerge(baseConfig,{
 devServer: {
     contentBase: './dist',
     inline: true, //是否实时监听，
     port: 8011 //指定端口
 }
}) 
```

###### (4)、prod.config.js配置

```js
const UglifyjsjsPlugin = require('uglifyjs-webpack-plugin')
const webpackMerge = require('webpack-merge')
const baseConfig = require('./base.config')
module.exports =webpackMerge(baseConfig,{
  plugins: [
    new UglifyjsjsPlugin() //发布的需要压缩js文件
  ]
}) 
```

###### (5)、配置package.json

```json
{
  "name": "demo",
  "version": "1.0.0",
  "main": "main.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1",
    "build": "webpack --config ./build/prod.config.js", //指定配置编译打包使用配置环境文件prod.config.js
    "dev": "webpack-dev-server --open --config ./build/dev.config.js" //指定配置编译打包使用配置环境文件
  },
  "author": "",
  "license": "ISC",
  "description": ""
}
```

###### (6)、base.config.js配置

```js
const path = require('path')
module.exports = {
    //入口
    entry: './src/main.js',
    //出口
    output:{
        path: path.resolve(_dirname,'../dist'),//配置打包到该文件的上一级上
        filename: 'bundle.js'
    }
}
```

#### 四、vue-cli脚手架

##### 1、vue-cli的安装

###### (1)、安装vue-cli3

```properties
npm install -g @vue/cli   #vue-cli依赖node.js与webpack  #这是脚手架3的安装方式
```

###### (2)、兼容vue-cli2

```properties
npm install -g @vue/cli-init #可使用该命令使vue-cli2兼容vue-cli3版本,可使用vue-cli的模板
```

###### (3)、vue-cli2初始化项目

```properties
vue init webpack 项目名 #创建项目
```

###### (4)、vue-cli3初始化项目

```properties
vue create 项目名 #创建项目
```

###### (5)、项目文件作用解析

```gfm
.babelrc  # 用于适配各种浏览器的配置以及es6转es5
.editorconfig  #编辑代码保存时格式调整配置
.gitignore  #git提交代码远程忽略那些个文件及文件夹
.eslintignore  #忽略一些文件中的代码不规范
.postcssrc.js  #css转化的所需配置文件
.gitkeep  #不管业务文件为不为空，都是能git上远程上
```

##### 2、compiler与only的区别

###### (1)、compiler的运行轨迹

```js
import Vue from 'vue'
import App from './App'
new Vue({
    el: '#app',
    template: '<App/>',
    components: {App}  //compiler:解析template转换为ast树，编译ast过后通过render函数实现虚拟dom，最后在页面展示UI
})
```

###### (2)、only的运行轨迹

```js
import Vue from 'vue'
import App from './App'
new Vue({
    el: '#app',
    render: h ->h(App) //only:通过render函数实现虚拟dom，直接在页面展示UI；这个运行更快打包更小
})
```

##### 3、vue-cli3的创建与结构

###### (1)、创建项目

```properties
vue create 项目名 #创建项目
```

