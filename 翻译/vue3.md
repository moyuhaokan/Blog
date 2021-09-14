vue 3 - 新特性，重大更新 和迁移方法



vue 3 发布以来，每个人都在想着进快迁移和尽快开始使用它。VUE 3 发布了不少新特性的同时做了很多提升性能和更小的体积使得这个版本成为客户端框架的真正候选者。注意，新语法，废弃的语法和一些重大的改变让你





mounting





你遇到的第一件事就是初始化你的应用的方式变了。在 VUE 2 你用 有渲染功能的VUE 构造函数并且有



```js
import Vue from 'vue'import App from './app.vue'

const app = new Vue({
  render: (h) => h(App),
}).$mount('#app')
```



在 vue 3中使用简单且优雅的语法



```js
import { createApp } from "vue";import App from "./App.vue";createApp(App).mount("#app");
```





这个跟 VUE2 在大多数情况下并没有太大的不同，因为我们只会创建一个 VUE 实例，不过在 我们的测试的时候会有很大的差别。我们现在需要使用[ localVue pattern](https://stackoverflow.com/questions/61691507/the-necessity-of-localvue-to-include-components-in-jest) 来组织我们的每个测试都是跟别的独立的

Fragments



在 VUE 2 里面，多个根节点是不支持的，解决办法就是把代码都放在一个包裹节点上面。



<!-- Layout.vue -->

<template>
  <div>
    <header>...</header>
    <main>...</main>
    <footer>...</footer>
  </div>
</template>





在 VUE 3 ，组件可以拥有多个根节点，这个可以消除包裹元素写出更清晰的标签。



<!-- Layout.vue -->
<template>
  <header>...</header>
  <main>...</main>
  <footer>...</footer>
</template>

## 



## Teleport



一个不常遇到但非常难解决的问题就是如果你的组件需要加载到DOM中与 VUE 结构层次不同。



一个常见的场景是创建一个组件包含了一个全屏的遮罩层。在大多数情况下，你希望遮罩层的逻辑存在于组件中，但是遮罩层的位置很快就很难通过CSS来解决，或者需要更改组件的的属性

使用这个teleport新特性可以很容易达到我们想要的效果。

```js
app.component('app-modal', {
  template: `
    <button @click="isOpen = true">
        Open modal
    </button>    <teleport to="body">
      <div v-if="isOpen" class="modal">
          I'm a teleported modal
      </div>
    </teleport>
  `,
  data() {
    return { 
      isOpen: false
    }
  }
})
```

你仍然像组件一样使用交互并且传递 props 给他

## Emits



发出事件的方式没有改变，但是你可以像这样在组件中声明发出事件

export default {
  name: 'componentName',
  emits: ['eventName']
}



这个不是强制的但应该考虑成最佳实践因为这使得成为自我节点的。

## Key Attributes



这个 Key 属性的作用是提示 VUE 虚拟节点来追踪节点的独立性。所以，VUE 知道何时重用节点和修补节点和何时重构节点或者重新创建他们。











## Composition API



一个很有争议的话题就是 2019年六月新的基于函数的组合 API，这和现有的 options api 有很大的区别引起了很大的争议和迷惑。当然好消息是options api 还可以使用，这一切都是因为在大型项目中使用 mixin 来做的话，会引起很多的复杂的问题。



新的组合 API 设计是为了更好的使用逻辑组件，封装，重用使其更可扩展，高效，更易追踪每个组件的属性。



 

下面的例子组件如何使用新的 API 来组织代码的。



<template>
  <button @click="increment">
    Count is: {{ state.count }}, double is: {{ state.double }}
  </button>
</template>

<script>
import { reactive, computed } from 'vue'

export default {
  setup() {
    const state = reactive({
      count: 0,
      double: computed(() => state.count * 2)
    })

​    function increment() {
​      state.count++
​    }

​    return {
​      state,
​      increment
​    }
  }
}
</script>



这个弊端就是需要花额外的实际来学习它，因为它跟vue2的不同的。好处是你不需要使用新的 API 来重写你的组件，你并不需要在所有地方都使用它。





## Functional Components



函数组件是不推荐的，主要的原因是使用函数组件可以提升性能但现在组件实例化和编译是的这些区别微不足道。这个改变会需要我们做很多手动迁移工作。









Scoped slots

这个改变可能会使你比较痛苦，那就是移除了scoped slots.合并到了 slots.



// Vue 2 Syntax
this.$scopedSlots.header

// Vue 3 Syntax
this.$slots.header()



Event Bus





 $on, $ once , $ and $off 这几个已经从 VUE 实例里面移除。 所以 VUE 3 不能创建一个 event bugs。 VUE 官方文档推荐是用 mitt 库。 这是一个小型但提供了 VUE 2 相同 api 的库。



Filters

在 vue3 里面 filters 别移除了。你可以在插件里面实现一个通过的功能。但是过滤器的管道与Javascript按位运算符冲突的事实意味着带过滤器的表达式无效。这就是为什么推荐使用方法来替代。



```js
// Vue 2 Syntax
{{ msg | format }}// Vue 3 Alternative
{{ format(msg) }}
```



这样子做的弊端是：链接多个方法不像链接多个过滤器那么优雅，但是代价又没这么小。

```js
// Vue 2 Syntax
msg | uppercase | reverse | pluralize
// Vue 3 Alternative
pluralize(reverse(uppercase(msg)))
```



异步组件



以前，异步组件的创建都是简单定义一个函数组件并且返回一个 Promise。



```js
const asyncPage = () => import('./NextPage.vue')const asyncPage = {
  component: () => import('./NextPage.vue'),
  delay: 200,
  timeout: 3000,
  error: ErrorComponent,
  loading: LoadingComponent
}
```





现在，在 vue3里面，函数组件是定义为纯函数。异步组件定义需要明确的定义为在包裹在一个新的**defineAsyncComponent**里面。



```js
import { defineAsyncComponent } from 'vue'// Async component without options
const asyncPage = defineAsyncComponent(() => import('./NextPage.vue'))// Async component with options
const asyncPageWithOptions = defineAsyncComponent({
  loader: () => import('./NextPage.vue'),
  delay: 200,
  timeout: 3000,
  errorComponent: ErrorComponent,
  loadingComponent: LoadingComponent
})
```















组件生命周期

 beforeDestroy 和 destroyed  生命周期被重名为beforeUnmount & unmounted。

```js
Vue 2.x
<script>
export default {
  beforeDestroy() {
    console.log('beforeDestroy has been called')
  }
  destroyed() {
    console.log('destroyed has been called')
  }
}
</script>Vue 3.x
<script>
export default {
  beforeUnmount() {
    console.log('beforeUnmount has been called')
  }
  unmounted() {
    console.log('unmounted has been called')
  }
}
</script>
```





IE11 支持



IE 11 在主版本已经不支持了。如果你不幸要支持它，你需要添加一些额外的文件来 polyfill 来代理它。

vuex 



vuex4 也已经伴随着 VUE 3 发布了。api 都是和以前一样并且代码会兼容前一个版本。失望吗？大可不必！ 这是一件不容易的事情。VUE 5 即将到来，举个例子：会移除 mutation 和嵌套模块。



## Migration plan to Vue 3



1.阅读官方的迁移指南

2.使用 mitt 库替代 eventbus



3. 升级 scoped slots 为普通的 slots
4. 使用方法替代过滤器
5. 升级到 vue2.7--这个版本会弃用跟 VUE 3 部件用新特性且会引导你怎么处理每个特性。
6. 升级到 VUE 3

你可能需要记住一点就是这可能需要比较漫长的过程并且花费一年。取决于你的项目大小和你当前使用了多少不推荐的特性。这可能优先级不高但是大幅度提升性能并且使用新的组合 API ，这个工作值得去做。