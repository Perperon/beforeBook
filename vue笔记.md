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

I、通过props向子组件传递数据

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

II、通过自定义事件向父组件发送消息

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

III、props的驼峰标识

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

IIII、双向绑定案例

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

IIIII、双向绑定案例-watch监听实现

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



###### (2)、子组件访问父组件$parent

