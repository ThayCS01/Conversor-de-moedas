<template>
  <div class="conversor">
    <h2>{{moedaA}} To {{moedaB}}</h2>
    <input type="text" v-model="moedaA_value" v-bind:placeholder="moedaA">
     <!--v-bind:placeholder para acessar o valor | v-model acessar o valor da moedaA -->
    <input type="button" value="Converter" v-on:click="converter">
    <h2>{{moedaB_value}}</h2>
  </div>
</template>

<script>
  export default {
    name: 'ConversorMoedas',
    props: ['moedaA', 'moedaB'],
       data() {
        
        return {
          moedaA_value: "",
          moedaB_value: 0,
        };
      },
      methods:{

        converter(){
          let de_para = this.moedaA + " " + this.moedaB

          let url = "http://free.currencyconverterapi.com/api/vS/convert?q=" + 
          de_para +
          "&compact=y";
        
        fetch(url).then(resp =>{
          return resp.json()
          })
          .then(json=>{
            let cotacao = json[de_para].val;
            this.moedaB_value = (cotacao * parseFloat(this.moedaA_value)).toFixed(2)

          })



        }
      



      
    }
  }

</script>

<style scoped>


</style>