<template>
  <div>

    <h2>hello table</h2>
    <div v-for="(title,index) in titles" :key="index">
      <h3>{{ title }}</h3>
      <ul v-for="(val,index) in valToJSON" :key="index">
        <li>
          <input id="index" v-model="val[title.toLowerCase()]" @change="someHandler"/>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
export default {
  name: "Table",
  props: ['titles', 'valToJSON'],
  methods: {
    someHandler(e, index) {
      // eslint-disable-next-line no-debugger
      // debugger
      console.log(e.currentTarget.value)
      console.log(index)

    },
  },
  data() {
    return {
      va: null,
      liitem: null
    }
  },


}

</script>

<style scoped>

</style>
