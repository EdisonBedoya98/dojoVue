<template>
  <div id="app">
    <h1>Traductor</h1>
    <translateIn v-on:formSubmit="traducirtexto"></translateIn>
    <translateOut v-text="traduciresteTexto"></translateOut>
  </div>
</template>

<script>
import translateIn from "./components/translateIn.vue";
import translateOut from "./components/translateOut.vue";
export default {
  name: "app",
  components: {
    translateIn,
    translateOut
  },
  data:function(){
    return{
      traduciresteTexto:''
    }
  },
  methods: {
    traducirTexto: function(texto,idioma) {
      this.$http
        .get(
          `https://translate.yandex.net/api/v1.5/tr.json/translate?key=trnsl.1.1.20190622T213455Z.f67e95598c7aee64.c0c49d0594aa527178d83c8e3c1a81ed05709a56&lang=${idioma}&text=${texto}` 
           
        )
        .then(response => {
          this.traduciresteTexto = response.body.text[0];
        });
    }
  }
};
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
