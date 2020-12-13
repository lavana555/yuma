<template>
  <div id="app">

    <HelloWorld />
    <TextArea />

  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'
import TextArea from "@/components/TextArea";
// import TableBootsrap from "@/components/TableBootsrap";

export default {
  name: 'App',
  components: {
    // TableBootsrap,
    TextArea,
    HelloWorld
  }
}
</script>

<style>

</style>
