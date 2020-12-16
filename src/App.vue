<!-- Representa el html (Estructura) -->
<template>
  <div id="app">
    <div class="header">
      <!-- <img src="/assets/contador3.png" alt="logo">  -->
      <h1>Contador a la Mano</h1>
        <nav>
          <button v-on:click="init" v-if="is_auth" > Registro </button> 
          
          <button v-on:click="getBalance" v-if="is_auth" > Balance </button> 
          <button v-on:click="getTipo" v-if="is_auth" > Reporte por tipo </button>
        </nav>
      </div>

    <div class="main-component">
      
      <router-view> </router-view>
    </div>

    <div class="footer">
      <h2>G3M2_9</h2>
    </div>
  </div>

</template>

<!-- Representa el js (Comportamiento) -->
<script>
  export default {
    name: 'App',
    components: {},
    data: function(){
      return {
        is_auth: localStorage.getItem('isAuth') || false
      }
    },
    
    methods: {
      init: function(){
        if(this.$route.name != "user"){
        let username = localStorage.getItem("current_username")
        this.$router.push({name: "user", params: {username:username}})
      }  

    },

      getBalance: function(){
        if(this.$route.name != "user_balance"){
          let username = localStorage.getItem("current_username")
          this.$router.push({name:"user_balance", params:{username:username}})
          }
      },

      getTipo: function(){
        if(this.$route.name != "reporte_tipo"){
          let username = localStorage.getItem("current_username")
          this.$router.push({name:"reporte_tipo", params:{username:username}})
          
          }
      },
    },

    beforeCreate: function(){
      localStorage.setItem('current_username', '1')
      localStorage.setItem('isAuth', true)
      this.$router.push({name: "user", params:{username:'1'}})
    } 
}

</script>

// Representa el css (estilo) -->
<style>
body{
  margin: 0 0 0 0;
}

.header{
  margin: 0%;
  padding: 0;
  width: 100%;
  height: 10vh;
  min-height: 100px; background-color: #984CF5 ; color:#E5E7E9 ;
  display: flex;
  justify-content: space-between; align-items: center;
}

.header h1{
  width: 20%;
  text-align: center;
}

.header nav {
  height: 100%;
  width: 45%;
  display: flex; 
  justify-content: space-around; 
  align-items: center;
  font-size: 20px;
}

.header nav button{
  color: #E5E7E9;
  background: #A564F5;
  border: 1px solid #45F5DA;
  border-radius: 5px;
  padding: 10px 20px;
}

.header nav button:hover{
  color: #4d229c; 
  background: #E5E7E9; 
  border: 1px solid #E5E7E9;
}

.main-component{
  height: 75vh;
  margin: 0%;
  padding: 0%;
  background: #FDFEFE ;
}
.footer{
  margin: 0;
  padding: 0;
  width: 100%;
  height: 10vh;
  min-height: 100px; 
  background-color: #984CF5; 
  color: #E5E7E9;
}

.footer h2{
  width: 100%;
  height: 100%;
  display: flex; 
  justify-content: center; 
  align-items: center;
}


</style>
