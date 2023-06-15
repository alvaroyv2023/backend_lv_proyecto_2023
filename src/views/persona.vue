<template>
      <h1>{{ titulo }}</h1>
      <p>{{ personas }}</p>
      <h1>{{ titulo }}</h1>
      <table border="1">
            <tr>
                  <td>ID</td>
                  <td>NOMBRE</td>
                  <td>EDAD</td>
            </tr>
            <tr v-for="per in personas" :key="per.id">
                  <td>{{ per.id }}</td>
                  <td>{{ per.nombre }}</td>
                  <td>{{ per.edad }}</td>
            </tr>
      </table>

  </template>
  <script>
import axios from "axios";
import {ref} from "vue"

 
      export default {
            /*data(){
                  return {
                        titulo: "Lista de personas",
                        personas: ["prueba"]
                  }

            }*/
            setup(){

                  //declarar variables
                  const titulo = ref("Lista de Personas")
                  let personas = ref([])

                  /*
                  axios.get("http://10.1.201.110:8000/api/persona").then(
                        (res) => {
                              console.log(res.data);
                              personas.value = res.data
                        }
                        
                  );
                  */
                  const listarPersonas = async () => {
                        try{
                        const res = await axios.get("http://10.1.201.110:8000/api/persona");
                        personas.value = res.data
                       }catch(error){
                        console.log(error);
                       }

                  }

                  listarPersonas();
                  // callback 
                  // antes se usaba collback es como un if anidado se soluciono con promesas 

                  // retornar variables y metodos 
                  return {
                        titulo,
                        personas
                  }
            }
            
      }

      // vuex es como una base de datos temporal , es como una memoria ram
</script>