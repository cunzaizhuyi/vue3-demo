<template>
    <div>
        {{ state}}
        <button @click="log">按钮</button>
    </div>
</template>

<script>
    import { ref, toRaw } from 'vue'; // 注意首字母小写
export default {
    name: 'ToRaw',

    // toRaw的作用：因为ref/reactive每次修改都更新UI，性能消耗大，若某些操作不需要UI及时更新，可以通过toRaw拿到原始数据
    // 对原始数据进行修改，这样UI就不会更新，性能就好了。
    // （当然也可以像下面那样，在定义ref/reactive的时候，就把原始变量user单独拿出去声明，直接修改user，跟修改userOld是一样的)）
    setup() {
        let age = 12;
        let state = ref(age);
        console.log('age === ref(age): ', age === state); // false。

        let ageOld = toRaw(state.value); // 一定要加.value，这是跟toRaw.vue区别的地方
        console.log('age === toRaw(state): ', age === ageOld); // true.

        let log = () => {
            // 改变原始数据，UI自然不会响应。（state.value不会变成15。）
            age = 15;
            console.log('111: ', state);
        };

        return { state, log };
    }
    // 对这种简单数据类型，toRaw好像意义不大？
};
</script>
<style>
    .ol{
        width: 300px;
        text-align: left;
    }
</style>
