<template>
    <div>
        <div>{{state.a.v}}</div>
        <div>{{state.a.b.v}}</div>
        <div>{{state.a.b.c.v}}</div>
        <div>{{state.a.b.c.d.v}}</div>
    </div>
    <button @click="log">按钮</button>
</template>

<script>

import { reactive } from 'vue';
export default {
    name: 'Recurse',
    setup() {
        // 不管是ref 还是 reactive 默认都是递归监听，性能消耗较大。
        // vue3对对象递归，每层的对象都封装了一个proxy对象
        let state = reactive({
            a: {
                v: 1,
                b: {
                    v: 2,
                    c: {
                        v: 3,
                        d: {
                            v: 4,
                        }
                    }
                }
            }
        });

        const log = () => {
            state.a.v = 'a';
            state.a.b.v = 'b';
            state.a.b.c.v = 'c';
            state.a.b.c.d.v = 'd';

            console.log('111: ', state.a);
            console.log('111: ', state.a.b);
            console.log('111: ', state.a.b.c);
            console.log('111: ', state.a.b.c.d);
        };

        return { state, log };
    },
};
</script>
