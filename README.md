# vue3-demo

练习vue3 新语法及API的使用


## 学习顺序

src/components下每一个.vue组件，都是一个vue3的知识点。

按照下面的顺序学习效果更佳


#### 组合API部分
* Ref.vue  组合API中ref()的简单使用
* Reactive.vue  组合API中reactive()的简单使用，一个todo list
* Reactive2.vue 除json和array外的其他对象
* Ref2.vue ref本质
* Which.vue 两个判断数据是哪种响应类型的API: isRef() & isReactive()
* Mix.vue 组合API和options API混合使用 及 组合API本质
* Lifecycle.vue 组合API的执行时机

* Recurse.vue 递归监听
* Recurse2.vue 非递归监听shallowRef() / shallowReactive()

* toRaw.vue 对reactive()返回对象进行toRaw()
* toRaw2.vue 对ref()返回对象toRaw()

* markRaw.vue 永远不想响应UI变化的数据，使用markRaw()

