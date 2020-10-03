
## vue3练手仓库

### 前言

vue3.0已经发布正式版，早晚都要学，赶早不赶晚。 

我的练手仓库
[GitHub](https://github.com/cunzaizhuyi/vue3-demo)

### Composition API
一组可以将UI 和 数据处理逻辑 分离的API。
入口函数setup();

#### ref() && reactive()
这两个函数，都可以把数据，变成响应式的。即，数据改变 驱动 视图（UI）改变。
其中。ref一般对简单数据类型进行响应，reactive对引用数据类型进行响应化。

先看下ref的例子

```
<template>
    <button @click="addCnt">count is: {{ cnt }}</button>
</template>

<script>
import { ref } from 'vue';
export default {
    name: 'Ref',
    // setup函数 是组合API(composition API) 的入口函数
    setup() {
        // 定义 变量/state。 注意ref()首字母小写，不是Ref。
        let cnt = ref(0); // ref只能监听简单类型数据的变化，不能监听复杂类型（对象/数组），复杂类型请用reactive()。

        // 定义 函数（方法）
        const addCnt = () => {
            // 注意必须加value
            cnt.value++;
        };

        // 在组合API中定义的变量/方法，想要在外部使用，必须return暴露出去
        return { cnt, addCnt };
    },
};
</script>
这是一个简单的 加法器 demo。我们用ref声明一个可响应状态cnt, 以及一个数据处理逻辑函数addCnt, 
setup()要求将状态和方法返回，才能在模板里使用。

```

再来看reactive的例子，实现一个TODO list demo
```
<template>
    <form>
        姓名：<input type="text" v-model="state.name">
        年龄：<input type="text" v-model="state.age">
        <input type="submit" @click="submit"></input>
    </form>
    <ol class="ol">
        <li v-for="(item, index) in state.students" :key="index" @click="delStu(index)">
            {{ item.name }} -- {{ item.age }}
        </li>
    </ol>
</template>

<script>
import { reactive } from 'vue'; // 注意首字母小写
export default {
    name: 'Reactive',

    // 入口函数
    setup() {
        // 声明几个变量，用reactive监听变化。
        let state = reactive({
            students: [
                {
                    name: '张三',
                    age: 11,
                },
                {
                    name: '李四',
                    age: 21,
                },
            ],
            name: '',
            age: '',
        });

        // 添加一个学生
        let submit = (e) => {
            e.preventDefault();
            state.students.push({
                name: state.name,
                age: state.age,
            });
            state.name = '';
            state.age = '';
        };

        // 删除一个学生
        let delStu = (index) => {
            state.students.splice(index, 1);
        };
        return { state, submit, delStu };
    }
};
</script>
```


#### 混合使用options api和composition API

composition API 当然是可以和以前的options API写法混用的。
实际上，composition API也叫注入API，是将setup中暴露的变量和方法注入到data()和methods中去。

```
<template>
    <div>
        {{ count }}
        <button @click="logCount">点击Count</button>
    </div>
    <div>
        {{ cnt }}
        <button @click="logCnt">点击Cnt</button>
    </div>
</template>

<script>
import { ref } from 'vue';
export default {
    name: 'Mix',
    data() {
        return {
            count: 1,
        };
    },
    methods: {
        logCount() {
            alert(this.count);
        }
    },
    // Vue2.x的写法叫做 Options API写法
    // 本🌰可见，组合API和Options API可以混用。
    // 且实际上，组合API（也叫注入API）是将其中的变量和方法注入到data()和methods中去
    setup() {
        let cnt = ref(5);
        let logCnt = () => {
            alert(cnt.value); // 注意ref监听的对象，在js中使用要加.value。
        };
        return { cnt, logCnt };
    }

};
</script>

```

#### isRef() && isReactive()

如何区分一个数据或者状态，是通过ref还是reactive包装的呢？
可以通过isRef 和 isReactive 两个方法进行判断。

```
<template>
    <button @click="log"> 按钮 </button>
</template>

<script>
import { ref, reactive, isRef, isReactive } from 'vue';
export default {
    name: 'Which',
    setup() {
        let age = ref(18);
        let state = reactive({
            age: 11
        });

        const log = () => {
            console.log('age is ref ? ', isRef(age)); // true
            console.log('age is reactive ? ', isReactive(age)); // false
            console.log('state is ref ? ', isRef(state)); // false
            console.log('state is reactive ? ', isReactive(state)); // true
        };

        return { age, log };
    },
};
</script>
```

在这个例子里，age是通过ref包装的，state是通过reactive包装的，可以通过isRef和isReactive区分。

#### shallowRef() && shallowReactive()

默认情况下，ref和reactive包装的数据都是 递归监听的，因而可以递归响应。
但是递归监听对性能是有影响的。
那么，假设要监听的数据数据量很大，且嵌套结构特别深，如果想要只对第一层数据监听，就可以使用shallowReactive()。

```
<template>
    <div>
        <div>{{state.age}}</div>
        <div>{{state.a.v}}</div>
        <div>{{state.a.b.v}}</div>
    </div>
    <button @click="log">按钮</button>
</template>

<script>
import { reactive, shallowReactive, shallowRef } from 'vue';
export default {
    name: 'Recurse',
    setup() {
        // 只需要将reactive改成shallowReactive，就可以非递归监听
        // 一般情况下，使用默认的递归监听即可，只有传入的数据量较大的时候，才考虑非递归监听
        let state = shallowReactive({
            a: {
                v: 1,
                b: {
                    v: 2,
                }
            },
            age: 15
        });

        const log = () => {
            // 注意观察 注释掉下面这句话 和 不注释下面这句话 的区别。
            // state.age = 16; // 只有age修改可以引起UI变化，若age不修改，内层数据修改，UI不变；若age和内存数据都修改，UI都变，是因为age的变化带动了内层数据UI的响应
            state.a.v = 'a';
            state.a.b.v = 'b';

            console.log('111: ', state);
            console.log('111: ', state.a);
            console.log('111: ', state.a.b);
        };
        return { state, log };
    },
};
</script>

```

#### toRaw() && markRaw()

还是上面那个问题，如果监听的数据数据量很大，而ref和reactive包装后，数据又都是实时反映到UI上的，那么，有可能
是对性能有所影响的。

如果不想对某些数据或状态的修改，都进行UI上的实时响应变化，该怎么办呢？
toRaw 和 markRaw也许可以帮到你。

toRaw 和 markRaw的区别是：toRaw是可以把某个可响应数据/状态，反取到原始值，修改原始值，则不会UI实时变化；
而markRaw则是直接将变量或状态声明为不可响应的，则后面，即使加了ref、reactive这样的包装，UI也不会再响应数据的变更。


先来看看toRaw

```
<template>
    <div>
        {{ state.name}} -- {{ state.age }}
        <button @click="log">按钮</button>
    </div>
</template>

<script>
import { reactive, toRaw } from 'vue'; // 注意首字母小写
export default {
    name: 'ToRaw',

    // toRaw的作用：因为ref/reactive每次修改都更新UI，性能消耗大，若某些操作不需要UI及时更新，可以通过toRaw拿到原始数据
    // 对原始数据进行修改，这样UI就不会更新，性能就好了。
    // （当然也可以像下面那样，在定义ref/reactive的时候，就把原始变量user单独拿出去声明，直接修改user，跟修改userOld是一样的)）
    setup() {
        let user = {
            name: 'zs',
            age: 12,
        };
        let state = reactive(user);
        console.log('user === reactive(user): ', user === state); // false。 他们是引用关系

        let userOld = toRaw(state);
        console.log('user === toRaw(state): ', user === userOld); // true.

        let log = () => {
            // 改变原始数据，UI自然不会响应。（不过因为是引用关系，state.name其实已经变成lisi了。）
            user.name = 'lisi';
            console.log('111: ', state);
        };

        return { state, log };
    }
};
</script>
```

再来看看markRaw

```
<template>
    <div>
        {{ state.name}} -- {{ state.age }}
        <button @click="log">按钮</button>
    </div>
</template>

<script>
import { reactive, markRaw } from 'vue'; // 注意首字母小写
export default {
    name: 'MarkRaw',

    setup() {
        let user = {
            name: 'zs',
            age: 12,
        };

        // 注意加 和 不加markRaw 区别。有了它，UI永不响应数据的变化。（虽然数据本身已经变了）
        markRaw(user);

        // 即使后面再用reactive包装改变量，UI也不响应数据变更。
        let state = reactive(user);

        let log = () => {
            state.name = 'lisi';
            console.log('111: ', state);
        };

        return { state, log };
    }
};
</script>
```

### 后记

该仓库 持续更新中，欢迎star~~~

[GitHub](https://github.com/cunzaizhuyi/vue3-demo)