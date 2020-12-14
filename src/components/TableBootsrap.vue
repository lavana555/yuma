<template>
  <div class="tabl_btsrp">
  <table class="table table-hover table-dark" v-for="(header,index) in headers" :key="index" >
    <thead >
    <tr>
      <th scope="col">{{header}}</th>

       </tr>
    </thead>
    <tbody v-for="(val,index) in objectJSON" :key="index">
    <tr>
      <td>
        <input id="index" v-model="val[header.toLowerCase()]" />
      </td>
      </tr>
    </tbody>
  </table>
  </div>
</template>

<script>
export default {
name: "TableBootsrap",
  props: ['headers', 'objectJSON'],
}
</script>

<style scoped>
.tabl_btsrp{
  display: flex;
}
.table{
  border-radius: 15px;
  margin: 0 auto;
  max-width: 300px !important;
  margin-top: 30px;
  border-top:none !important;
  text-align: center;
  margin-left: 7px
}
</style>
