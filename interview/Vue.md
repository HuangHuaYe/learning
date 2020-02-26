# Vue

## v-show 与 v-if

- v-if 是真正的条件渲染,如果初始条件为假,则什么都不渲染,也就是惰性的(lazy).如果v-if是作用在vue组件,组件在切换中会有完整的生命周期.**开销大**
- v-show 不管初始条件是什么都会渲染,然后通过display属性开控制现实.**开销小**.适合频繁切换的场景.

## 生命周期

## 父子生命周期顺序

- 渲染过程

    父 beforeCreate -> 父 created -> 父 beforeMount -> 子 beforeCreate -> 子 created -> 子 beforeMount -> 子 mounted -> 父 mounted

- 更新过程

    父 beforeUpdate -> 子 beforeUpdate -> 子 updated -> 父 updated

- 销毁过程

    父 beforeDestroy -> 子 beforeDestroy -> 子 destroyed -> 父 destroyed

## 监听子组件的生命周期事件

    <Child @hook:mounted="do" />

## KeepAlive

keep-alive是内置的一个组件,可以使被包含的组件保留状态,只是隐藏起来,避免被重新渲染.

- `include`,`exclude`配置,支持字符串和正则.`exclude`的优先级高
- 有两个钩子函数: `actived`,`deactived`

原理:

- 在`render`函数中获取内部的`slot`,然后根据组件的id和tag生成缓存key.
- 将组件的`keepAlive`属性设置为`true`
- 自身存在属性`abstract: true`他的父组件在初始化生命周期的时候会跳过.
- 在vue渲染的`patch`阶段会吧缓存的dom直接插入到父元素之中.

## Vue组件间通讯

1. props / $emit
2. ref / $parent / $children
3. EventBus 创建一个空的Vue实例作为中央事件总线.
4. $attrs / $listenners 
5. provide / inject
6. vuex

## vue-router 模式

1. hash
2. history
3. abstract

## 双向绑定原理

有下面三个概念:

- `Observer`,监听器

    利用`Object.defineProperty` 定义`getter`,`settter`,每个属性的`getter`都会持有一个`Dep`的实例.

- `Watcher`,订阅者

    负责更新视图,从`Dep`获取数据更新通知.在初始化的将自身推入`Dep`的收集里面

- `Dep`,订阅器

    收集订阅着(`Watcher`)在数据变更的时候(`Observer`)通知`Watcher`更新视图.

## Proxy与Object.defineProperty优劣

**Proxy 的优势如下:**

- Proxy 可以直接监听对象而非属性；
- Proxy 可以直接监听数组的变化；
- Proxy 有多达 13 种拦截方法,不限于 apply、ownKeys、deleteProperty、has 等等是 Object.defineProperty 不具备的；
- Proxy 返回的是一个新对象,我们可以只操作新的对象达到目的,而 Object.defineProperty 只能遍历对象属性直接修改；
- Proxy 作为新标准将受到浏览器厂商重点持续的性能优化，也就是传说中的新标准的性能红利；

**Object.defineProperty 的优势如下:**

- 兼容性好，支持 IE9，而 Proxy 的存在浏览器兼容性问题,而且无法用 polyfill 磨平，因此 Vue 的作者才声明需要等到下个大版本( 3.0 )才能用 Proxy 重写。

## 虚拟DOM

[深入剖析：Vue核心之虚拟DOM](https://juejin.im/post/5d36cc575188257aea108a74#heading-1)

## 未来Vue3.0的变化

- 检测机制,使用`Proxy`实现监听器.
- 模版.未来Vue会推荐使用api来直接生成vdom
- 使用Typescript开发
-