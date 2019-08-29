# 可能触及你盲区的Vue知识总结

<a name="JfIGg"></a>
## 概述
先思考以下几个问题，带着这几个问题了解并学习Vue：

1. vue是什么？
1. vue解决了哪些问题？
1. vue周边生态有哪些？
<a name="BYvEG"></a>
## 1. Vue.js是什么
> Vue是一套用于构建用户界面的渐进式框架。与其它大型框架不同的是，Vue 被设计为可以自底向上逐层应用。Vue 的核心库只关注视图层，不仅易于上手，还便于与第三方库或既有项目整合。另一方面，当与[现代化的工具链](https://cn.vuejs.org/v2/guide/single-file-components.html)以及各种[支持类库](https://github.com/vuejs/awesome-vue#libraries--plugins)结合使用时，Vue 也完全能够为复杂的单页应用提供驱动。（来自官网的解释）


基础篇的语法部分可以直接到[vue官方网](https://cn.vuejs.org/)站或者[GitHub查看](https://github.com/vuejs/vue)

_**以下涉及的demo地址在 **__**[GitHub](https://github.com/geektime-geekbang/geektime-vue-1/tree/master/%E6%BC%94%E7%A4%BADEMO%E6%BA%90%E7%A0%81)(点我)**_
<a name="ZsiBY"></a>
## 2. vue组件的核心概念
<a name="Sk7M3"></a>
### 2.1 属性
![78876b0a7262847ad6433024c01fc9ba.jpeg](https://cdn.nlark.com/yuque/0/2019/jpeg/152654/1566022109583-c9d09a12-aac2-4589-8c6c-60714a36699a.jpeg#align=left&display=inline&height=420&name=78876b0a7262847ad6433024c01fc9ba.jpeg&originHeight=920&originWidth=1635&size=90356&status=done&width=746)

<a name="STICg"></a>
### 2.2 事件
<a name="LZTbM"></a>
#### 2.2.1 普通事件
包括@click,@input,@change,@xxx 等事件，在子组件通过this.@emit('xxx',...) 触发
<a name="1bNnu"></a>
#### 2.2.2 修饰符事件
包括@click.stop,@input.trim()等，一般用于原生HTML元素，自定义组件需要自行开发支持
<a name="ROSVo"></a>
### 3. 插槽
普通插槽和作用于插槽<br />注意版本的区别
> 在 2.6.0 中，我们为具名插槽和作用域插槽引入了一个新的统一的语法 (即 `v-slot` 指令)。它取代了 `slot` 和 `slot-scope` 这两个目前已被废弃但未被移除且仍在[文档中](https://cn.vuejs.org/v2/guide/components-slots.html#%E5%BA%9F%E5%BC%83%E4%BA%86%E7%9A%84%E8%AF%AD%E6%B3%95)的特性。


```json
<template>
  <div>
    <slot />
    <slot name="title" />
    <slot name="item" v-bind="{ value: 'vue' }" />
  </div>
</template>

<script>
export default {
  name: "SlotDemo"
};
</script>
```

**_也可以参考我去年在公众号写的一篇关于插槽的_**[**_文章_**](https://mp.weixin.qq.com/s?__biz=MzIyNTA0MTgyNQ==&mid=2652499623&idx=1&sn=a56970532e34f4c2be76a748a630d2f9&chksm=f3e88269c49f0b7f87949eed19d507538e73ce6bb449aaef4eab35734eedcf186e1072fc95d0&mpshare=1&scene=1&srcid=&sharer_sharetime=1566023825789&sharer_shareid=e6790037cb11ed4491ce2a4fa33b83fd&key=904260214fdf08297b23c357d8e4bd503dbf41cf3d1fe50ac7340f50dcecec39af7e4294daedf939564d198636d31a3498e8135ca067b35ce655e2b5c5d71412fa8558d6b715e6ffb49dc1f11de480a1&ascene=1&uin=MjY2ODcyMjM2MA%3D%3D&devicetype=Windows+10&version=62060833&lang=zh_CN&pass_ticket=29aUeuZ76ddW6vJ1uIUn7y%2BhQZQlZujzjWDIdOU60BRhv8WxZ7Oy7%2FT%2BMHFSVasI)**_(是兄弟就来点我吧)_**

<a name="8U5z6"></a>
### 4. 双向绑定or单向数据流
<a name="jlJYS"></a>
#### 4.1 什么是双向绑定
![微信图片_20190817152406.png](https://cdn.nlark.com/yuque/0/2019/png/152654/1566026685564-130ad66f-d9ae-4805-a00e-6f7b014a4428.png#align=left&display=inline&height=207&name=%E5%BE%AE%E4%BF%A1%E5%9B%BE%E7%89%87_20190817152406.png&originHeight=207&originWidth=582&size=12523&status=done&width=582)
<a name="jUV1l"></a>
#### 4.2 什么是单向数据流
      ![TIM截图20190817152327.png](https://cdn.nlark.com/yuque/0/2019/png/152654/1566026734925-ba7255c2-163f-40bb-8971-e23d0914af36.png#align=left&display=inline&height=193&name=TIM%E6%88%AA%E5%9B%BE20190817152327.png&originHeight=193&originWidth=540&size=9973&status=done&width=540)
<a name="7eWPu"></a>
#### 4.3 So

- Vue是单向数据流，不是双向绑定
- Vue的双向绑定不过是语法糖
- Object.defineProperty是用来做响应式更新的，和双向绑定没有关系

_v-model_ 只是语法糖

```html
<input v-model="something">
```
这不过是以下示例的语法糖：
```html
<input
  v-bind:value="something"
  v-on:input="something = $event.target.value">
```

目前sync修饰符一样可以实现双向绑定，在原理上和v-model差不多
<a name="hLzcq"></a>
### 5. 虚拟DOM (Virtual DOM)
<a name="RwfwW"></a>
#### 5.1 virtual DOM和真实DOM的区别
Virtual DOM是将真实的DOM的数据抽取出来，以对象的形式模拟树形结构。比如dom是这样的：

```html
<div>
    <p>123</p>
</div>
```

对应的Virtual DOM（伪代码）：
```javascript
var Vnode = {
    tag: 'div',
    children: [
        { tag: 'p', text: '123' }
    ]
};
```
<a name="TdalR"></a>
#### 5.2 理解Virtual DOM 
Virtual DOM主要采用diff算法，在比较新旧节点的时候，比较只会在同层级进行, 不会跨层级比较。<br />![TIM截图20190817144726.png](https://cdn.nlark.com/yuque/0/2019/png/152654/1566026250757-92fa5126-3b02-4008-b624-981f66cbb0c5.png#align=left&display=inline&height=374&name=TIM%E6%88%AA%E5%9B%BE20190817144726.png&originHeight=681&originWidth=1208&size=226779&status=done&width=664)
<a name="Dl8xx"></a>
#### 5.3 diff流程图
当数据发生改变时，set方法会让调用Dep.notify通知所有订阅者Watcher，订阅者就会调用patch给真实的DOM打补丁，更新相应的视图<br />![998023-20180519212357826-1474719173.png](https://cdn.nlark.com/yuque/0/2019/png/152654/1566026326608-9973a5ee-ff9e-4d3f-a8e6-64e59f44beec.png#align=left&display=inline&height=680&name=998023-20180519212357826-1474719173.png&originHeight=680&originWidth=920&size=18545&status=done&width=920)<br />vue的算法实现可以参考 GitHub源码 [https://github.com/vuejs/vue/tree/dev/src/core/vdom](https://github.com/vuejs/vue/tree/dev/src/core/vdom) 
<a name="LzVGm"></a>
#### 5.4 v-for 中加:key值的作用
vue中列表循环需加:key="唯一标识" 唯一标识可以是item里面id index等，因为vue组件高度复用增加Key可以标识组件的唯一性，为了更好地区别各个组件 key的作用主要是为了高效的更新虚拟DOM

<a name="omTTG"></a>
## 3. Vue生态篇
<a name="tyh2T"></a>
### 3.1 Vuex
> Vuex 是一个专为 Vue.js 应用程序开发的**状态管理模式**。它采用集中式存储管理应用的所有组件的状态，并以相应的规则保证状态以一种可预测的方式发生变化。

<a name="93S9q"></a>
#### 3.1.1 Vuex运行机制
![vuex.png](https://cdn.nlark.com/yuque/0/2019/png/152654/1566029543514-8e14c9bb-bbe9-4bb2-90b7-afc82bdfb11a.png#align=left&display=inline&height=551&name=vuex.png&originHeight=551&originWidth=701&size=8112&status=done&width=701)
<a name="jcvfE"></a>
#### 3.1.2 Vuex底层原理

- State: 提供统一的响应式数据源
- Getter: 借助Vue的计算属性computed来实现缓存
- Mutation: 更改state方法
- Action: 触发mutation方法
- Module: Vue.set 动态添加state到响应式数据中
<a name="zKcKB"></a>
#### 3.1.3 min-Vuex核心代码的实现

```javascript
import Vue from 'vue'
const Store = function Store (options = {}) {
  const {state = {}, mutations={}} = options
  this._vm = new Vue({
    data: {
      $$state: state
    },
  })
  this._mutations = mutations
}
Store.prototype.commit = function(type, payload){
  if(this._mutations[type]) {
    this._mutations[type](this.state, payload)
  }
}
Object.defineProperties(Store.prototype, {
  state: { 
    get: function(){
      return this._vm._data.$$state
    } 
  }
});
export default {Store}
```

<a name="eVLsW"></a>
### 3.2 Vue Router
<a name="CFvmx"></a>
#### 3.2.1 解决的问题

- 监听url的变化，并在变化前后执行相应的逻辑
- 不同的url 对应不同的组件
- 提供多种方式改变url的API（URL的改变不能导致浏览器的刷新）
<a name="j1r6K"></a>
#### 3.2.2 路由类型

- Hash模式 URL不够优雅 无法使用锚点定位
- History模式 需要后端配合，IE9不兼容
<a name="sGd69"></a>
#### 3.2.3 底层原理
![TIM截图20190817163739.png](https://cdn.nlark.com/yuque/0/2019/png/152654/1566031102958-13a677b5-b367-4854-a128-db2fd8346767.png#align=left&display=inline&height=231&name=TIM%E6%88%AA%E5%9B%BE20190817163739.png&originHeight=231&originWidth=705&size=37365&status=done&width=705)
<a name="2K5Ij"></a>
### 3.3 Nuxt
<a name="bRdO0"></a>
#### 3.3.1 Nuxt 解决了哪些问题（SPA的缺点）

- 利于SEO优化，爬虫对页面的抓取 （SSR服务端渲染）
- 降低首屏渲染时长 （预渲染）
<a name="TZs5P"></a>
#### 3.3.2 Nuxt底层原理
![TIM截图20190817164622.png](https://cdn.nlark.com/yuque/0/2019/png/152654/1566031635788-27291730-76f4-4f1f-a0f9-8b97bad3d147.png#align=left&display=inline&height=544&name=TIM%E6%88%AA%E5%9B%BE20190817164622.png&originHeight=544&originWidth=1574&size=198324&status=done&width=1574)

<a name="rankL"></a>
### 3.4 工具配置
<a name="9P2na"></a>
#### 3.4.1 VS Code编辑器下的配置

- EsLint 代码校验 避免一些低级错误
- prettier 格式美化

setting.json 文件下eslint的保存自动符合eslint规则配置

```json
{
   "window.zoomLevel": 1,
    "files.autoSave":"off",
    "eslint.validate": [
       "javascript",
       "javascriptreact",
       "html",
       { "language": "vue", "autoFix": true }
     ],
     "eslint.options": {
        "plugins": ["html"]
     },
     //为了符合eslint的两个空格间隔原则
   "editor.tabSize": 2,
   "eslint.alwaysShowStatus": true,
   "eslint.autoFixOnSave": true,
   "terminal.integrated.rendererType": "dom"
}
```

<a name="Bf5BB"></a>
## 4.单元测试
<a name="al30v"></a>
### 4.1 安装Jest
![TIM截图20190817165745.png](https://cdn.nlark.com/yuque/0/2019/png/152654/1566032390935-f35947e8-d150-4974-af9e-7cfd554aa2b1.png#align=left&display=inline&height=354&name=TIM%E6%88%AA%E5%9B%BE20190817165745.png&originHeight=354&originWidth=850&size=275566&status=done&width=850)
<a name="qd5mV"></a>
### 4.2 配置
jest.config.js 

```javascript
module.exports = {
  moduleFileExtensions: ["js", "jsx", "json", "vue"],
  transform: {
    "^.+\\.vue$": "vue-jest",
    ".+\\.(css|styl|less|sass|scss|svg|png|jpg|ttf|woff|woff2)$":
      "jest-transform-stub",
    "^.+\\.jsx?$": "babel-jest"
  },
  transformIgnorePatterns: ["/node_modules/"],
  moduleNameMapper: {
    "^@/(.*)$": "<rootDir>/src/$1"
  },
  snapshotSerializers: ["jest-serializer-vue"],
  testMatch: [
    "**/tests/unit/**/*.spec.(js|jsx|ts|tsx)|**/__tests__/*.(js|jsx|ts|tsx)"
  ],
  testURL: "http://localhost/"
};

```
<a name="6NXxG"></a>
### 4.3 对计数器组件单测

```javascript
import { mount } from "@vue/test-utils";
import Counter from "@/components/Counter.vue";
import sinon from "sinon";

describe("Counter.vue", () => {
  const change = sinon.spy();
  const wrapper = mount(Counter, {
    listeners: {
      change
    }
  });
  it("renders counter html", () => {
    expect(wrapper.html()).toMatchSnapshot();
  });
  it("count++", () => {
    const button = wrapper.find("button");
    button.trigger("click");
    expect(wrapper.vm.count).toBe(1);
    expect(change.called).toBe(true);
    button.trigger("click");
    expect(change.callCount).toBe(2);
  });
});

```
<a name="Aom8i"></a>
## 5. 组件的发布
<a name="22KNe"></a>
### 5.1 详见 [**内网私有化npm包注册上传流程**](https://www.yuque.com/vmenggd/note/rs9mf2)
<a name="Qda4t"></a>
## 参考资料

- [https://time.geekbang.org/course/intro/163](https://time.geekbang.org/course/intro/163)
- [https://vue-test-utils.vuejs.org/zh/](https://vue-test-utils.vuejs.org/zh/)
- [https://cn.vuejs.org/](https://cn.vuejs.org/)
- [https://github.com/vuejs/vue/tree/dev/src/core/vdom](https://github.com/vuejs/vue/tree/dev/src/core/vdom)
<a name="Vy57d"></a>
## 补充说明
适合有一定vue开发经验的同学阅读，原理性介绍较多，我学完这门课程之后，对vue的机制，思想和单元测试有了更深的了解，解了一些自己的疑惑，有些内容介绍不是很细致，如果你想细致或者深入的了解某方面的知识，可以留言，有时间可以一起探讨
