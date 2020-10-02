<template>
    <div>
        <div>{{state.age}}</div>
        <div>{{state.a.v}}</div>
        <div>{{state.a.b.v}}</div>
        <div>{{state.a.b.c.v}}</div>
        <div>{{state.a.b.c.d.v}}</div>
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
                    c: {
                        v: 3,
                        d: {
                            v: 4,
                        }
                    }
                }
            },
            age: 15
        });

        const log = () => {
            // 注意观察 注释掉下面这句话 不注释下面这句话 的区别。
            // state.age = 16; // 只有age修改可以引起UI变化，若age不修改，内层数据修改，UI不变；若age和内存数据都修改，UI都变，是因为age的变化带动了内层数据UI的响应
            state.a.v = 'a';
            state.a.b.v = 'b';
            state.a.b.c.v = 'c';
            state.a.b.c.d.v = 'd';

            console.log('111: ', state);
            console.log('111: ', state.a);
            console.log('111: ', state.a.b);
            console.log('111: ', state.a.b.c);
            console.log('111: ', state.a.b.c.d);
        };

        return { state, log };
    },
};
</script>
