<template>
    <div>
        {{ state.time }}
        <button @click="fn">按钮</button>
    </div>
</template>

<script>
    import { reactive } from 'vue'; // 注意首字母小写
export default {
    name: 'Reactive2',

    // 入口函数
    setup() {
        let state = reactive({
            // 如果给reactive传递了 其他对象，不能响应，若想响应，可以重新赋值的方式
            time: new Date()
        });

        let fn = () => {
            // 这样不行。 虽然打印出来是加了一天，但是UI不能响应更新
            // state.time.setDate(state.time.getDate() + 1);
            // console.log('111: ', state.time)

            // 重新赋值的方式, 就可以
            const newTime = new Date(state.time.getTime());
            newTime.setDate(state.time.getDate() + 1);
            state.time = newTime;

        };
        return { state, fn };
    }
};
</script>
<style>
</style>
