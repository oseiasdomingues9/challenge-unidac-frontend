<template>  
    <section>
        <nav aria-label="breadcrumb">
            <ol class="breadcrumb mt-1 ms-2">
                <li class="breadcrumb-item"><a href="/">Collaboradores</a></li>
                <li class="breadcrumb-item active" aria-current="page">Cadastrar</li>
            </ol>
        </nav>
        <div class="container custom-container">            
            <form class="col-7" action="/" @submit.prevent="saveBreakfast">               
                <div class="mb-3">
                    <label for="name" class="form-label">Nome</label>
                    <input type="text" class="form-control" id="name" name="name" placeholder="Digite seu nome" required v-model="collaboradores.name">
                </div>
                <div class="mb-3">
                    <label for="cpf" class="form-label">CPF</label>                    
                    <input type="tel" pattern=".{14}" v-mask="'###.###.###-##'" class="form-control" id="cpf" name="name" placeholder="Digite seu cpf" required v-model="collaboradores.cpf">
                </div>
                <p>O que você vai trazer?</p>
                <div v-for="food of collaboradores.foods" :key=food.id>         
                    <input type="text" class="form-control mb-2" placeholder="Item" name="name"  v-model="food.name" >
                </div>          
                <button type="submit" class="btn btn-primary">Salvar</button>   
                <small class="ms-3 text-danger">{{error}}</small>
            </form>
        </div>
    </section>
</template>

<script>

import api from '../services/api'

export default {
  name: "form",

  data(){
      return{
         collaboradores:{
             name: '',
             cpf: '',
             foods: [{
                name: ''
         },
         {
                name: ''
         },{
                name: ''
         }]                         
                  
      },
      error: ''
      }
  },
  methods:{

      saveBreakfast(){
        api.insertBreakfast(this.collaboradores)
        .catch(e =>{
            this.error = e.response.data.message;
        }).then(error =>{if(error.data == ''){
          window.location.href = "/"
        }})
      }
  }
  
}

</script>

<style scoped>
.custom-container{
    display: flex;
    justify-content: center;
}

</style>
