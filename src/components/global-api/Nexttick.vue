<template>
    <div>
        next tick
    </div>
</template>

<script>
    import { nextTick } from 'vue';
    export default {
        name: "nexttick",
        mounted() {
            // nextTick 已经变成实例API，不再是全局API。this.$nextTick() 或者 Vue.nextTick
            nextTick(() => {
                console.log('111: ', '可以可以')
            })
        }
    }
</script>

<style scoped>

</style>