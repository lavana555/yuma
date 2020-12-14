<template>
  <div>
    <h2>LoadCSV</h2>
    <input type="file" id="file" ref="file" v-on:change="handleUploadFile">
  </div>
</template>

<script>
export default {
  name: "LoadData",
  props: ['getToCSV'],
  data() {
    return {
      file: '',
      reader: null,
      contents: null,
      element: null,
      objectJSON: null,
      lines: null,
      headers: [],
    }
  },

  methods: {
    handleUploadFile() {
      const self = this;
      this.file = this.$refs.file.files[0]
      this.reader = new FileReader();
      this.reader.onload = function (e) {
        this.contents = e.target.result
        this.lines = this.contents.split("\n");
        var result = []
        this.headers = this.lines[0].replace(/['"«»]/g, '').split(",");
        for (var i = 1; i < this.lines.length; i++) {
          var obj = {};
          var currentline = this.lines[i].replace(/['"«»]/g, '').split(",");
          for (var j = 0; j < this.headers.length; j++) {
            obj[this.headers[j]] = currentline[j];
          }
          result.push(obj);
        }
        this.objectJSON = JSON.stringify(result)
        console.log('jsonObejsct', this.objectJSON)
        debugger
        self.$emit('getToCSV', this.objectJSON)
        return this.objectJSON;
      }
      this.reader.readAsText(this.file)
    },
  }
}

</script>

<style scoped>

</style>
