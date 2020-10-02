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
            console.log('age is ref ? ', isRef(age));
            console.log('age is reactive ? ', isReactive(age));
            console.log('state is ref ? ', isRef(state));
            console.log('state is reactive ? ', isReactive(state));
        };

        return { age, log };
    },
};
</script>
