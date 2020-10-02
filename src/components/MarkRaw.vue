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

        let state = reactive(user);

        let log = () => {
            state.name = 'lisi';
            console.log('111: ', state);
        };

        return { state, log };
    }
};
</script>
<style>
    .ol{
        width: 300px;
        text-align: left;
    }
</style>
