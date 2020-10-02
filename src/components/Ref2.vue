<template>
    <button @click="addAge">age is: {{ age }}</button>
    <button @click="addAge">age is: {{ age }}</button>

</template>

<script>

import { ref } from 'vue';
export default {
    name: 'Ref',
    setup() {
        // ref只是reactive的一种适用于简单类型的简写。
        // 本质还是reactive()。相当于 ref(18) ---> reactive({ value: 18 })
        let age = ref(18); // ref只能监听简单类型数据的变化，不能监听复杂类型（对象/数组），复杂类型请用reactive()。

        const addAge = () => {
            //ref注意点： 在JS中 必须加value，在HTML中不用加value
            age.value++;
        };

        return { age, addAge };
    },
};
</script>
