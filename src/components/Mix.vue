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
