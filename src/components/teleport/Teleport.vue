<template>
    <div>
        <button @click="visible = true">打开对话框</button>

        <!-- dialog -->
        <teleport to="body">
            <div v-if="visible" class="model">
                <div>
                    这是对话框里面的内容。父元素是body
                    <button @click="visible = false">点我关闭对话框</button>
                </div>
            </div>
        </teleport>
    </div>
</template>

<script>
    // 该组件只有一个必需的prop，命名为to。它接受必须是有效查询选择器或HTMLElement（如果在浏览器环境中使用）的字符串。
    // <teleport to="#some-id" />
    // <teleport to=".some-class" />
    // <teleport to="[data-portal]" />
    export default {
        name: 'Ref',
        data() {
            return {
                visible: false,
            }
        }
    };
</script>
<style>
    .model{
        position: absolute;
        top: 0;
        right: 0;
        bottom: 0;
        left: 0;
        background-color: rgba(0,0,0,0.5);
        display: flex;
        flex-direction: column;
        align-items: center;
        justify-content: center;
    }
    .model div{
        width: 300px;
        height: 300px;
        background-color: #fff;
        padding: 10px;
    }
</style>
