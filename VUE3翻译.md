





  vue 是一个高速发展的用来生成单页面应用的开源前端框架。由于vue对于开发人员友好的语法，易使用，著名的好上手的文档，所以受欢迎程序一直在增加并不断或者新用户的喜爱。在2020年11月，vue的第三个版本，vue3 发布， 它更小，更易维护，且有更多的新特性



vue3有什么更新？ 我注意到 vue 3有如下新特性，组合 API vue当中的一个允许我们创建大的应用在更小，更容用的组件上。这让我们更容易管理开发过程。在vue2上，我们有三种方式复用代码



### MIXIN 

 优势



按照功能组织



限制



容易发生冲突： 我们可能在某些属性上发生命名冲突。

交互方式不清晰

不是那么容易复用，在我们想要配置 mixin 跨其它组件的时候。





### MIXIN  factories



mixin  factories 函数是我们定制的 mixin 函数，我们通过传入参数来修改 mixin。



优势



容易复用，我们可以配置代码且指定 mixin 的交互逻辑。



限制：

不能动态配置，因为在运行时没有实例。





命名需要强制约定



他们有额外的隐藏属性： 我们需要识别出那些属性是导出的。

不是那么容易复用，在我们想要配置 mixin 跨其它组件的时候。



### scoped slots



我们可以复用模板通过slots 可这个特殊的类型传递数据，不需要重复渲染元素。

优点：



几乎解决了 MIXIN 的所有缺点。



限制：

你配置的最终模板，理想情况下包含的内容应该是我们想要渲染的。



有作用域的插槽会增加模板的缩进量，降低阅读性。



暴露的属性只能在模板中使用。

游戏我们使用的是 3 个组件而不是一个，所以性能会降低。





正如你看到的，我们有个多个选择项。但是每个都有限制。 在 VUE2 中，我们写的组件可以通过组织组件的选项 ： 组件，props，data，computed，methods， 声明周期。但是在这个过程中，我们的单个组件会变得越来越大，难以阅读和并且在将来难以维护。





VUE 3 提供的一个新特性运行我们通过逻辑关注点来组织组件 - 这个新特性就走组合 API。这是一个可选项，运行我们使用更高级的语法，你记住是一个可选性，可以使用旧的方式。







组合 API 给我们一个机会在不同的组件间复用代码。







VUE 2 通过 Options API 和 Mixin 来复用代码





<template>   <div id="app">     <div class="content">       <h1>{ {title} }</h1> 	<label for="title"> 	  <input type="text" name="title" v-model="inputVal" /> 	</label> 	<button @click="addTitle" class="add-btn">Add</button> 	<button @click="clearInput">Clear</button>       	<button @click="pressMe">Clear</button>     </div>   </div> </template>  <script> const exampleMixin = {   data() {     return {       someInfo: "This is our mixin!"     }   },   methods: {     pressMe() {       alert(this.someInfo);     }   } } export default {   mixins: [exampleMixin],   data() {     return { 	inputVal: "", 	title: ""     };   },   methods: {     clearInput() { 	this.inputVal = "";     },     addTitle() { 	this.title = this.inputVal;     }   } }; </script>



你可以看到，通常情况下我们使用 option 组件（data, methods）来组织我们的代码。



VUE 3 通过 组合 API 来组织代码。



<template>   <div id="app">     <div class="content">       <h1>{ {title} }</h1>       <label for="title">         <input type="text" name="title" v-model="inputVal" />       </label>       <button @click="addTitle" class="add-btn">Add</button>       <button @click="clearInput">Clear</button>     </div>   </div> </template>  <script>   import { ref } from "vue";  export default {   setup() {     const inputVal = ref("");     const title = ref("");      function clearInput() {       this.inputVal = "";     }      function addTitle() {       this.title = this.inputVal;     }      return { inputVal, title, clearInput, addTitle };   } }; </script>

组合 API 是VUE 3 给我们另一种复用代码的方式。这个功能有如下的优势和限制







优点

更少的代码，很方便的把功能从组件中抽离成函数。



建立在你早已熟系的函数航母。

比 mixin 和 slots 作用域。

只能感知，自动填充，当你在编写代码的时候提示你。



更好的 Typescript 支持，你生成的新项目可以在 VUE 3 中使用最新的是特性   。





### teleprot

   





早先是叫 protal ,Teleport允许我们在 某个父节点下面渲染我们的 HTML 代码。主要的优势是Teleport 可以把元素放在DOM 数上的任何一个地方。所以我们不需要嵌套组件或者在不同的组件放入不同的代码。



他接收的属性叫做"  to" ,这就是把我们想要的元素放到哪个地方。这个条件就是目标的元素需要组件加载后就已经存在了。





所以在 VUE 3 中看起来是这样子的

<teleport to="#app">  <div>Foo</div> </teleport> <teleport to="#app">  <div>Bar</div> </teleport>



编译成：

<div id="app">   <div>Foo</div>   <div>Bar</div> </div>



你可以在不同的地方插入节点，当然，我们需要知道的是，新增的阶段不会继承样式。



Teleport在我们想要设置一个特殊的节点在 DOM 树上面的时候特别有用。举个例子： 遮罩层，某些alert， 弹框。



某些组件的更新





如果你想在一个组件里面定义一个事件并发送到父组件上面我们有一个新的选项叫做“emit”，跟现有的 props 类型。

如果我们想要定义一个异步组件，我们可以使用defineAsyncComponent 函数。



VUE 2

 const  asyncComponent = () => import ('./AsyncComponent.vue')



vue 3



const  asyncComponent = defineAsyncComponent(() => import ('./AsyncComponent.vue'))









### Fragments



 在vue 2，我们不能拥有多个根节点，这是vue 2
  其中的一个限制如果我们创建多个的话会收到警告。 现在在vue 3
  里面，我们不需要包裹根节点在一个主节点上面---我们可以有在根上面拥有多个根节点。





vue 2



<template>  <div>    <header></header>    <section></section>  </div> </template>





VUE 3 

<template>  <header></header>  <section></section> </template>





过滤器从 VUE 3 中移除



  过滤器已经不支持了，而是，我们使用computer属性或者方法替代。

Vue 2



<template>  <div id="app">    <span>{ {  amount | usd  } }</span>  </div> </template> <script>  export default {    data() {      return {        amount: 10      }    },    filters: {      usd(val) {        return val + '$'            }    }  } </script>





VUE 3 



<template>  <div id="app">    <span>{ { usd } }</span>  </div> <template> <script> export default {  data() {    return {      amount: 10    }  },  computed: {    usd() {      return this.amount + '$'    }  } } </script>



  我们在vue 3中可以使用的生命周期如下：

 <template> render changes:  在新版本里面，<template>这个标签只有在特定的指令下才会渲染其内容，不然的话，就会当做一个正常的HTML标签，并渲染。
   

   ### 实验性的功能







VUE 3 运行我们设置一个被动的加载组件，叫做 Suspense 组件



Suspense 组件运行我们提供一下回调内容，当我们用户在等待数据的时候。这时候可以看到一下动态效果或者文字。





<Suspense>  <template #default>    *<!-- component/component which makes an asynchronous call -->*  </template>  <template #fallback>    *<!-- Content to display when loading -->*    Loading...  </template> </Suspense>





####实验性的 状态驱动的 CSS 变量





CSS 变量允许我们存储一个值在某个地方，然后可以在任何地方都可以复用。这是一个很好的方式让我们的写出更干净的代码。





在 VUE  3 中，单文件组件支持 v-bind 函数在 style 标签里面。所以我们就可以绑定组件的状态到人物的CSS 属性上面。这允许我们动态的更改某些 CSS 的属性。

Vue 3

```
<template>
  <div id="app">
    <div class="content">
       <h1>Hello world!</h1>
       <button @click="modalToggle">Click me</button>
    </div>
    <div v-if="showModal" class="modal">
      <h2>Modal window</h2>
      <button class="close-btn" @click="modalToggle">Close the window</button>
    </div>
    <div class="shadow"></div>
 </div>
</template>

<script>
export default {
  data() {
    return {
      displayShadow: "none",
      showModal: false
    };
  },
  methods: {
    modalToggle() {
      this.showModal = !this.showModal;
      this.displayShadow = this.showModal ? "block" : "none";
    }
  }
};
</script>

<style>
.shadow {
  display: v-bind(displayShadow);
  position: absolute;
  top: 0;
  left: 0;
  width: 100vw;
  height: 100vh;
  background: rgb(46 46 46 / 31%);
  z-index: 10;
  opacity: 1;
}
</style>
```



在上面的代码中，你可以看到这新特性。我们想要关闭或者显示m

odal  窗口取决于 modal 是否是 visible 。所以我们绑定displayShadow 这个值到display 这个属性的shadow 这个条件来更改他的值在modalToggle 这个方法里面。  他的作用就是关闭或者打开这个modal 窗口。







####单个文件组件的`<style scoped>` 更改



如果我们使用 scoped 在 SFC 上面，这意味着 CSS 只会在当前组件生效。这帮助开发者提供更一致的样式在单文件组件里面。

》》》  和 deep 组合器，已经被废弃了，我们可以使用::v-deep()或者更短的:deep()

如果我们不想组件被父组件和子组件影响样式，::v-slotted()`/`:slotted() 这个元素。这样子作用域的样式就不用影响组件了。







### Multiple v-models



在 VUE 中我们使用 v-model 来做双向数据绑定，最受欢迎的在元素上绑定 值的方式。在 VUE 2 中，我们在一个组件上只能使用一个 v-model ，但是在 VUE 3 中，我们可以在组件上通过设置不同的名字设置不同的 v-model。让我们来看看吧。





VUE 2



```
<template>
  <div id="app">
    <exampleForm v-model="person" />
  </div>
</template>

<script>
export default {
  data() {
    return {
      person: {
        age: 20,
        name: "Jan"
      }
    };
  }
};
</script>
```

Vue 3

```
<template>
  <div id="app">
    <exampleForm v-model:age="person.age" v-model:name="person.name" />
  </div>
</template>

<script>
export default {
  data() {
    return {
      person: {
        age: 20,
        name: "Jan"
      }
    };
  }
};
</script>
```







### 声明周期

   destroyed声明周期我们重命名为unmounted。beforeDestroy生命周期我们改成了beforeUnmount，





| Options API (default) | Composition API (*hook inside* setup) |
| --------------------- | ------------------------------------- |
| beforeCreate          | Not needed                            |
| created               | Not needed                            |
| beforeMount           | onBeforeMount                         |
| mounted               | onMounted                             |
| beforeUpdate          | onBeforeUpdate                        |
| updated               | onUpdated                             |
| beforeUnmount         | onBeforeUnmount                       |
| unmounted             | onUnmounted                           |
| errorCaptured         | onErrorCaptured                       |
| renderTracked         | onRenderTracked                       |
| renderTriggered       | onRenderTriggered                     |



### <template> render changes

  

  在新版本里面，<template>这个标签只有在特定的指令下才会渲染其内容，不然的话，就会当做一个正常的HTML标签，并渲染。</template>





### 总结





我在这本篇文章里面只写了VUE 3 中的部分新特性。想要学习更多，我建议你看一下官方文档哈游最新的 VUE report 仓库。

















