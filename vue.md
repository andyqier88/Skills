概述
先思考以下几个问题，带着这几个问题了解并学习Vue：
vue是什么？
vue解决了哪些问题？
vue周边生态有哪些？
1. Vue.js是什么
Vue是一套用于构建用户界面的渐进式框架。与其它大型框架不同的是，Vue 被设计为可以自底向上逐层应用。Vue 的核心库只关注视图层，不仅易于上手，还便于与第三方库或既有项目整合。另一方面，当与现代化的工具链以及各种支持类库结合使用时，Vue 也完全能够为复杂的单页应用提供驱动。（来自官网的解释）
基础篇的语法部分可以直接到vue官方网站或者GitHub查看
以下涉及的demo地址在 GitHub(点我)
2. vue组件的核心概念
2.1 属性
2.2 事件
2.2.1 普通事件
包括@click,@input,@change,@xxx 等事件，在子组件通过this.@emit('xxx',...) 触发
2.2.2 修饰符事件
包括@click.stop,@input.trim()等，一般用于原生HTML元素，自定义组件需要自行开发支持
3. 插槽
普通插槽和作用于插槽
注意版本的区别
在 2.6.0 中，我们为具名插槽和作用域插槽引入了一个新的统一的语法 (即 v-slot 指令)。它取代了 slot 和 slot-scope 这两个目前已被废弃但未被移除且仍在文档中的特性。
也可以参考我去年在公众号写的一篇关于插槽的文章(是兄弟就来点我吧)
4. 双向绑定or单向数据流
4.1 什么是双向绑定
4.2 什么是单向数据流
      
4.3 So
Vue是单向数据流，不是双向绑定
Vue的双向绑定不过是语法糖
Object.defineProperty是用来做响应式更新的，和双向绑定没有关系
v-model 只是语法糖
这不过是以下示例的语法糖：
目前sync修饰符一样可以实现双向绑定，在原理上和v-model差不多
5. 虚拟DOM (Virtual DOM)
5.1 virtual DOM和真实DOM的区别
Virtual DOM是将真实的DOM的数据抽取出来，以对象的形式模拟树形结构。比如dom是这样的：
对应的Virtual DOM（伪代码）：
5.2 理解Virtual DOM 
Virtual DOM主要采用diff算法，在比较新旧节点的时候，比较只会在同层级进行, 不会跨层级比较。
5.3 diff流程图
当数据发生改变时，set方法会让调用Dep.notify通知所有订阅者Watcher，订阅者就会调用patch给真实的DOM打补丁，更新相应的视图
vue的算法实现可以参考 GitHub源码 https://github.com/vuejs/vue/tree/dev/src/core/vdom 
5.4 v-for 中加:key值的作用
vue中列表循环需加:key="唯一标识" 唯一标识可以是item里面id index等，因为vue组件高度复用增加Key可以标识组件的唯一性，为了更好地区别各个组件 key的作用主要是为了高效的更新虚拟DOM
3. Vue生态篇
3.1 Vuex
Vuex 是一个专为 Vue.js 应用程序开发的状态管理模式。它采用集中式存储管理应用的所有组件的状态，并以相应的规则保证状态以一种可预测的方式发生变化。
3.1.1 Vuex运行机制
3.1.2 Vuex底层原理
State: 提供统一的响应式数据源
Getter: 借助Vue的计算属性computed来实现缓存
Mutation: 更改state方法
Action: 触发mutation方法
Module: Vue.set 动态添加state到响应式数据中
3.1.3 min-Vuex核心代码的实现
3.2 Vue Router
3.2.1 解决的问题
监听url的变化，并在变化前后执行相应的逻辑
不同的url 对应不同的组件
提供多种方式改变url的API（URL的改变不能导致浏览器的刷新）
3.2.2 路由类型
Hash模式 URL不够优雅 无法使用锚点定位
History模式 需要后端配合，IE9不兼容
3.2.3 底层原理
3.3 Nuxt
3.3.1 Nuxt 解决了哪些问题（SPA的缺点）
利于SEO优化，爬虫对页面的抓取 （SSR服务端渲染）
降低首屏渲染时长 （预渲染）
3.3.2 Nuxt底层原理
3.4 工具配置
3.4.1 VS Code编辑器下的配置
EsLint 代码校验 避免一些低级错误
prettier 格式美化
setting.json 文件下eslint的保存自动符合eslint规则配置
4.单元测试
4.1 安装Jest
4.2 配置
jest.config.js 
4.3 对计数器组件单测
5. 组件的发布
5.1 详见 内网私有化npm包注册上传流程
参考资料
https://time.geekbang.org/course/intro/163
https://vue-test-utils.vuejs.org/zh/
https://cn.vuejs.org/
https://github.com/vuejs/vue/tree/dev/src/core/vdom
补充说明
适合有一定vue开发经验的同学阅读，原理性介绍较多，我学完这门课程之后，对vue的机制，思想和单元测试有了更深的了解，解了一些自己的疑惑，有些内容介绍不是很细致，如果你想细致或者深入的了解某方面的知识，可以留言，有时间可以一起探讨