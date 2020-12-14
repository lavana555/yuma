<template>
  <div class="form-group">
    <form v-on:submit.prevent="submit">
      <div class="form-group">
        <label for="exampleFormControlTextarea1">Enter your data</label>
        <textarea
            class="form-control" id="exampleFormControlTextarea1"
            @focus="handleBlur"
            cols=70 rows=5
            type="text"
            v-model="modelform" :placeholder="[[textPlaceholder]]"></textarea>
        <div class="error-value">
          <p>{{ error }}</p>
        </div>
      </div>
      <div class="btn-block">
        <button v-if="isFetching" type="button" class="btn btn-dark" @click="submit">Continue</button>
        <button v-if="!isFetching" type="button" class="btn btn-success" @click="setValue">Unload</button>
        <button  type="button" class="btn btn-success" @click="saveTocsv">saveToCSV</button>
      </div>
      <TableBootsrap
          v-bind:headers="headers"
          v-bind:objectJSON="objectJSON"
      />
    </form>
    <LoadData v-on:getToCSV="getToCSV"/>
  </div>

</template>

<script>
import TableBootsrap from "@/components/TableBootsrap";
import LoadData from "@/components/LoadData";

export default {
  name: "TextArea",
  components: {
    LoadData,
    TableBootsrap,
  },
  data() {
    return {
      formValue: null,
      modelform: null,
      objectJSON: null,
      headers: [],
      isFetching: true,
      newval: null,
      textPlaceholder: '[\n' +
          '    {"name":"...","year":"..."},\n' +
          '    {"name":"...","year":"..."}\n' +
          ']',
      regexp: '',
      error: null,
      jsonObject: null


    }
  },
  methods: {
    submit() {
      this.headers = []
      if (this.modelform === null) {
        this.error = 'incorrect value'
      } else {
        this.objectJSON = JSON.parse(this.modelform);
        this.objectJSON.forEach(object => {
          Object.keys(object).filter((el) => {
            let header = el.slice(0, 1).toUpperCase() + el.slice(1)
            this.headers.includes(header) ? '' : this.headers.push(header);
          })
          this.isFetching = !this.isFetching
        })
      }
    },
    getToCSV(objectJSON) {

      this.headers = []
      this.isFetching = !this.isFetching
      this.objectJSON = JSON.parse(objectJSON);

      this.objectJSON.forEach(object => {
        Object.keys(object).filter((el) => {
          let header = el.slice(0, 1).toUpperCase() + el.slice(1)
          this.headers.includes(header) ? '' : this.headers.push(header);
        })
        //this.isFetching = !this.isFetching
      })

    },
    handleBlur() {
      this.error = ''
    },
    setValue() {
      this.modelform = JSON.stringify(this.newval);
      this.isFetching = !this.isFetching
    },
    saveTocsv(){
      this.objectJSON = JSON.parse(this.modelform)
      console.log('objectJSON:',typeof(this.objectJSON))
      console.log('objectJSON:',this.objectJSON)
      const header = this.objectJSON.map((x) => Object.keys(x))
          .reduce((acc, cur) => (acc.length > cur.length ? acc : cur), []);

      // specify how you want to handle null values here
      const replacer = (key, value) => (
          value === undefined || value === null ? '' : value);
      let csv = this.objectJSON.map((row) => header.map(
          (fieldName) => JSON.stringify(row[fieldName], replacer)).join(','));
      csv = [header.join(','), ...csv];
      const csvObject=csv.join('\r\n');
       // csv.join('\r\n');
      console.log('csvObject:',csvObject)
      // var fs = require('fs');
      const csvBlob = new Blob([csvObject], { type: "text/csv" });
      const blobUrl = URL.createObjectURL(csvBlob);
      const anchorElement = document.createElement("a");

      anchorElement.href = blobUrl;
      anchorElement.download = "data.csv";
      anchorElement.click();
      // const fileWriter = new FileWriter("data.csv");
      // fileWriter.open() ;
      // fileWriter.writeLine("Another line") ;
      // fileWriter.close()
    }
  },
  watch: {
    objectJSON: function () {
      console.log('watch:', this.objectJSON)
      this.newval = this.objectJSON

    }
  }
}
</script>

<style scoped>
.form-group {

  max-width: 500px;
  margin: 0 auto;
  margin-bottom: 50px;
  margin-top: 50px;
}

.form-control {
  background-color: #343a40;
  color: white;
  border-radius: 15px;
}

.btn-block {
  display: flex;
  justify-content: space-between
}

.error-value {


  color: red;
}
</style>
