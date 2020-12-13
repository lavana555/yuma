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
      </div>
      <TableBootsrap
          v-bind:titles="titles"
          v-bind:objectJSON="objectJSON"
      />
    </form>
  </div>

</template>

<script>
import TableBootsrap from "@/components/TableBootsrap";

export default {
  name: "TextArea",
  components: {
    TableBootsrap,
  },
  data() {
    return {
      formValue: null,
      modelform: null,
      dataObject: [],
      objectJSON: null,
      titles: [],
      isFetching: true,
      newval: null,
      textPlaceholder: '[\n' +
          '    {"name":"...","year":"..."},\n' +
          '    {"name":"...","year":"..."}\n' +
          ']',
      regexp: '',
      error: null

    }
  },
  methods: {
    submit() {
      if (this.modelform === null) {
        this.error = 'incorrect value'

      } else {
        this.objectJSON = JSON.parse(this.modelform);
        this.objectJSON.forEach(element => {
          Object.keys(element).filter((item) => {
            let name = item.slice(0, 1).toUpperCase() + item.slice(1)
            this.titles.includes(name) ? '' : this.titles.push(name);
          })
          this.isFetching = !this.isFetching
        })
      }
    },
    handleBlur() {
      this.error = ''
    },
    setValue() {
      this.modelform = JSON.stringify(this.newval);
      this.isFetching = !this.isFetching
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
