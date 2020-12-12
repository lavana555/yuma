<template>
  <div>
  <table >
    <tr>
      <th>Name</th>
      <th>Year</th>

    </tr>
    <tr v-for="(data,index) in dataObject" :key="index">

      <td>{{data.name}}</td>
      <td>{{data.year}}</td>
    </tr>
     </table>
    <button @click="setDate">setData</button>
    </div>
</template>

<script>
export default {
  name: "Table",
  //props:['dataObject'],
  methods:{
    setDate(){
      alert(this.dataObject)
      console.log('table:',typeof (this.dataObject))
    }
  },
  // data(){
  //   return{
  //    dataObject: [{name:"Name 1",year:"2010"},{name:"Name 2",year:"1997"},{name:"Name 3",year:"2004"}]
  // }
  // }
}

</script>

<style scoped>

</style>
