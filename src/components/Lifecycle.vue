<template>
    <div>
        {{ count }}
        <button @click="logCount">点击Count</button>
    </div>
</template>

<script>
    import { ref } from 'vue';
export default {
    name: 'Lifecycle',
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
    // 表示组件刚刚被创建出来，data和methods还没初始化好
    beforeCreate(){
        console.log('before create: ', )
    },
    // 表示组件刚刚被创建出来，data和methods已经初始化好
    created(){
        console.log('created: ', )
    },
    // setup的执行时机在beforeCreate 和 created 之间。
    // 因此，在setup中，不能获取到data和methods中的东西
    setup() {
        // 为了避免我们错误的引用，Vue直接将setup中的this修改成了undefined
        // console.log('111: ', this); // undefined
        // console.log('111: ', this.data); // Cannot read property 'data' of undefined
        // console.log('111: ', this.methods); // Cannot read property 'methods' of undefined
        return {};
    }

};
</script>
