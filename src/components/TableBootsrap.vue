<template>
  <div>
  <table class="table table-hover table-dark" v-for="(title,index) in titles" :key="index" >
    <thead >
    <tr>
      <th scope="col">{{title}}</th>

       </tr>
    </thead>
    <tbody v-for="(val,index) in valToJSON" :key="index">
    <tr>
      <td>
        <input id="index" v-model="val[title.toLowerCase()]" />
      </td>
      </tr>
    </tbody>
  </table>
  </div>
</template>

<script>
export default {
name: "TableBootsrap",
  props: ['titles', 'valToJSON'],
}
</script>

<style scoped>
.table{
  margin: 0 auto;
  max-width: 300px !important;

}
</style>
