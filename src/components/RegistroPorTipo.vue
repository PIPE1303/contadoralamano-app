<template>
    <div id="RegistroTipo">
       
         
            <nav>
            <button v-on:click="getIngreso" v-if= "true" > Ingresos </button> 
            <button v-on:click="getEgreso" v-if= "true" > Egresos </button> 
            </nav>
       
            <h2> Hola <span> {{username}} </span> </h2>
            <h2>Aqui tienes tus registros de <span> {{registro_tipo}} </span></h2>
            <h2>tu observacion fue <span>{{nota}} </span> </h2>
            <h2>Información de las Ordenes ordinarias <span>{{registro[0].nota}}</span></h2>
            <table>
                <tr>
                    <th>id</th>
                    <th>fecha</th>
                    <th>usuario</th>
                    <th>tienda</th>
                    <th>valor</th>
                </tr>
            </table>
        
        </div>
</template>

<script> 
    import axios from'axios';
    export default {
        name: 'RegistroTipo',
        data: function(){
            return { 
                username:"", 
                Balance:"", 
                nota:"",
                registro_tipo:"egreso",
                tipo:"",
                registro: [
                    {
                        id:"1", 
                        id_usuario:"6", 
                        tipo:"", 
                        valor: 2600, 
                        fecha:"10-12-2020", 
                        etiqueta:"comida", 
                        nota:"pina"
                        
                    }
                ]
                
        }
        },
        methods: {
             getIngreso: function(){
            this.username = this.$route.params.username
            this.registro_tipo="ingreso"  
            let self = this
            axios.get("http://localhost:8000/registro/tipo/" + this.username + "?Tipo=" + this.registro_tipo) // + this.username
                .then((result) => {
                    //self.Balance = result.data.Balance
                    this.nota="vamos del putas"
                })
                .catch((error) => {
                    alert("ERRORServidor");
                });      
        },

            getEgreso: function(){
                this.username = this.$route.params.username
                this.registro_tipo="egreso"  
                let self = this
                axios.get("http://localhost:8000/registro/tipo/" + this.username + "?Tipo=" + this.registro_tipo) // + this.username
                    .then((result) => {
                        //self.Balance = result.data.Balance
                        this.nota="la eatamos coronando"
                    })
                    .catch((error) => {
                        alert("ERRORServidor");
                    });         
        },
        },

       

        created: function(){
            this.username = this.$route.params.username
            
            let self = this
            axios.get("http://localhost:8000/registro/tipo/" + this.username + "?Tipo=" + this.registro_tipo) // + this.username
                .then((result) => {
                    //self.Balance = result.data.Balance
                    this.nota="vamos bien"
                })
                .catch((error) => {
                    alert("ERRORServidor");
                });
         
        }
    }                      
</script>    

<style>
#RegistroTipo{
    width:100%;
    height:100%;
    display:flex;
    flex-direction:column;
    justify-content:center;
    align-items:center;
}
#RegistroTipo h2{
    font-size:30px;
    color:#283747;
}

#RegistroTipo span{
    color:crimson;
    font-weight:bold;
}
</style>