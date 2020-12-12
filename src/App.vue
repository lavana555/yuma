<template>
  <div id="app">

    <HelloWorld />
    <TextArea />
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'
import TextArea from "@/components/TextArea";

export default {
  name: 'App',
  components: {
    TextArea,
    HelloWorld
  }
}
</script>

<style>

</style>
