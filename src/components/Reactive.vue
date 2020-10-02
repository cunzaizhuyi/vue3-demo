<template>
    <form>
        姓名：<input type="text" v-model="state.name">
        年龄：<input type="text" v-model="state.age">
        <input type="submit" @click="submit"></input>
    </form>
    <ol class="ol">
        <li v-for="(item, index) in state.students" :key="index" @click="delStu(index)">
            {{ item.name }} -- {{ item.age }}
        </li>
    </ol>
</template>

<script>
    import { reactive } from 'vue'; // 注意首字母小写
export default {
    name: 'Reactive',

    // 入口函数
    setup() {
        // 声明几个变量，用reactive监听变化。
        let state = reactive({
            students: [
                {
                    name: '张三',
                    age: 11,
                },
                {
                    name: '李四',
                    age: 21,
                },
            ],
            name: '',
            age: '',
        });

        // 添加一个学生
        let submit = (e) => {
            e.preventDefault();
            state.students.push({
                name: state.name,
                age: state.age,
            });
            state.name = '';
            state.age = '';
        };

        // 删除一个学生
        let delStu = (index) => {
            state.students.splice(index, 1);
        };
        return { state, submit, delStu };
    }
};
</script>
<style>
    .ol{
        width: 300px;
        text-align: left;
    }
</style>
