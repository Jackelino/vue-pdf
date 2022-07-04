<script>
import HelloWorld from './components/HelloWorld.vue';
import pdfMake from "pdfmake/build/pdfmake";
import pdfFonts from "pdfmake/build/vfs_fonts";

pdfMake.vfs = pdfFonts.pdfMake.vfs;
export default {
  name: 'App',
  components: {
    HelloWorld
  },
  data() {
    return {
      animals: [
        ['Column 1', 'Column 2', 'Column 3', 'Column 4']
      ]
    }
  },
  methods: {
    exportPdf() {
      let docDefinition = {
        content: [
          {
            layout: 'lightHorizontalLines', // optional
            table: {
              // headers are automatically repeated if the table spans over multiple pages
              // you can declare how many rows should be treated as headers
              headerRows: 1,
              widths: ['*', 'auto', 100, '*'],

              body: this.animals
            }
          }
        ]
      };
      const pdf = pdfMake.createPdf(docDefinition)
      pdf.download()
    }
  }
}


</script>

<template>
  <img alt="Vue logo" src="./assets/logo.png"/>
  <HelloWorld msg="Hello Vue 3 + Vite"/>
  <button v-on:click.prevent="exportPdf()">Pdf</button>
</template>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
