<template>
  <div>
    <h2>TextArea</h2>

    <textarea id="TTP"
              cols=50 rows=10
        v-model="data" placeholder="enter please your JSON object" ></textarea>
    <button @click="continuebtn">Continue</button>
    <Table  v-bind:dataObject="dataObject"/>
  </div>
</template>

<script>
import Table from "@/components/Table";
export default {
name: "TextArea",
  components: {Table},
  data(){
  return{
   // dataaaa:'[{name:"Name 1",year:"2010"},{name:"Name 2",year:"1997"},{name:"Name 3",year:"2004"}]',
    dataaaa:'[{"name":"Name 1","year":"2010"},{"name":"Name 2","year":"1997"},{"name":"Name 3","year":"2004"}]',
    //dataObject:[{name:"Name 1",year:"2010"},{name:"Name 2",year:"1997"},{name:"Name 3",year:"2004"}]
    dataObject:[],
    results:null,
    information:null,
    numbers : '[0, 1, "2", 3]',
    numberMas:[],
    numberMass:[]

  }
  },
  methods:{
    continuebtn(){
console.log(typeof (this.numbers))
      this.numberMas=JSON.parse(this.numbers)
      console.log('type:',typeof (this.numberMas))
      console.log('mas:',this.numberMas)
   console.log(typeof(this.dataaaa))
//d=this.dataaaa.split()
      for (var i=0; i<dataArray.length; i++){
        dataArray[i] = JSON.parse(dataArray[i]);
        console.log(dataArray[i]);
       this.numberMass=JSON.parse('[{ 1,2010}]')
  //     console.log('type:',typeof (this.numberMas))
  //     console.log('mas:',this.numberMas)
      //  this.information = document.getElementById("TTP");
      //  this.results=JSON.parse('information')
      // console.log('resultstype:',typeof (this.results))
      // console.log('results:',typeof (this.results))
    //   alert(typeof(this.data))
    //   console.log('data',this.data)
    //   this.dataObject = JSON.parse(this.data); // парсим пользовательскую строку, в этот момент отрисовываются карточки
    // console.log('dsfsd:',this.dataObject)
      // this.dataObject.forEach(element => { // заполняем titles, отрисовываюся заголовки карточек
      //   Object.keys(element).filter((item) => {
      //     let name = item.slice(0,1).toUpperCase() + item.slice(1)
      //     this.titles.includes(name)? '': this.titles.push(name);
      //   })
      // })



    },

  },

}
</script>

<style scoped>

</style>
