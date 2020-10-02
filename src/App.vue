<template>
<!--  <img alt="Vue logo" src="./assets/logo.png" />-->
<!--  <Ref/>-->
<!--  <Ref2/>-->
<!--  <Reactive></Reactive>-->
<!--  <Reactive2></Reactive2>-->
<!--  <Mix></Mix>-->
<!--  <Lifecycle></Lifecycle>-->
  <which />
</template>

<script>
import Ref from './components/Ref.vue'
import Ref2 from './components/Ref2.vue'
import Reactive from './components/Reactive.vue'
import Reactive2 from './components/Reactive2.vue'
import Mix from './components/Mix.vue'
import Lifecycle from './components/Lifecycle.vue'
import Which from './components/Which.vue'

export default {
  name: 'App',
  components: {
    Ref,
    Ref2,
    Reactive,
    Reactive2,
    Mix,
    Lifecycle,
    Which,
  }
}
</script>
