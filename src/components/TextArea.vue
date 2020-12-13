<template>
  <div class="form-group">
    <form v-on:submit.prevent="submit">
      <div class="form-group">
        <label for="exampleFormControlTextarea1">Enter your data</label>
        <textarea
            class="form-control" id="exampleFormControlTextarea1"

            cols=70 rows=2
            type="text"
            v-model="modelform" placeholder="enter please your JSON object"></textarea>
      </div>
      <button type="button" class="btn btn-dark" @click="submit">Continue</button>
      <button type="button" class="btn btn-success" @click="setValue">Watch completed</button>
      <!--    <Table-->
      <!--        v-bind:titles="titles"-->
      <!--        v-bind:valToJSON="valToJSON"-->
      <!--    />-->
      <TableBootsrap
          v-bind:titles="titles"
          v-bind:valToJSON="valToJSON"
      />
    </form>
  </div>

</template>

<script>
//import Table from "@/components/Table";
import TableBootsrap from "@/components/TableBootsrap";

export default {
  name: "TextArea",
  components: {
    TableBootsrap,
    //Table
  },
  data() {
    return {
      formValue: null,
      modelform: null,
      dataObject: [],
      results: null,
      information: null,
      numberMas: [],
      numberMass: [],
      valToJSON: null,
      titles: [],
      isFetching: true,
      newval: null

    }
  },
  methods: {
    submit() {
      this.valToJSON = JSON.parse(this.modelform);
      this.valToJSON.forEach(element => {
        Object.keys(element).filter((item) => {
          let name = item.slice(0, 1).toUpperCase() + item.slice(1)
          this.titles.includes(name) ? '' : this.titles.push(name);
        })
      })

    },
    setValue() {
      this.modelform = JSON.stringify(this.newval);

    }
  },
  watch: {
    valToJSON: function () {
      console.log('watch:', this.valToJSON)
      this.newval = this.valToJSON
      //this.isFetching=!this.isFetching
    }
  }
}
</script>

<style scoped>
.form-group {
  max-width: 500px;
  margin: 0 auto;
}

</style>
