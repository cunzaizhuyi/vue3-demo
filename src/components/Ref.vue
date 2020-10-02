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
