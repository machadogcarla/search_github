<template>
  <div>
    <div class="container">  

      <template v-if="mostrarDiv()">
        <div class="search card card-body" >
            <p class="titulo1">GitHub <span class="titulo2">Search</span></p>
            <form @submit="getUser">
                <div class="form-group row">
                  <input class="col-sm-11 col-form-label" type="text"  id="search" required/>
                  <div class="col-sm-1">
                    <button class="btn btn-dark btn-block"> <v-icon class="material-icons"> search </v-icon></button>
                  </div>
              </div>
            </form>  
        </div>
      </template>    
      
      
        <template v-else>
            <div class="search card card-body">
              <div class="row"> 
                  <div class="col-md-4">
                    <p class="titulo1peq">GitHub <span class="titulo2peq">Search</span></p>
                  </div> 
                  <div class="col-md-8">
                    <form @submit="getUser" >
                        <div class="form-group row">
                          <input class="col-sm-10 form-control form-control-sm" type="text"  id="search" required/>
                          <div class="col-sm-2">
                            <button class="btn btn-dark"> <v-icon class="material-icons"> search </v-icon></button>
                          </div>
                        </div>
                    </form>      
                </div>         
              </div>
          </div>
        </template>

            
      <section v-if="errored">
        <div class="alert alert-warning" role="alert">O usuário não foi encontrado. Tente novamente</div>
      </section>

        <template v-if="mostrarDivResult()">
          <div class="row mt-3" v-if="user.length !== 0">
          <div class="col-md-4">
            <Profile :user="user" />   
          </div>
          <div class="col-md-8">
            <Repos
              v-for="repo in orderedRepos"
              :repo="repo"
              :key="repo" 
            />
          </div>
        </div>
      </template>

    </div>
  </div>

</template>

<script>

import _ from 'lodash';
import axios from 'axios';
import Profile from "./components/Profile.vue";
import Repos from "./components/Repos.vue";

export default {

  name: "app",
  
  data() {

      return {
        valor: true,
        errored: false,
        valorResult: false,
        github: {
          url: "https://api.github.com/users",
          client_id: "3101ae14397bfa4010a2d",
          client_secret: "46fa1f407bc140a181b2f013bab033b954e23a18",
          count: "30",
          },
        user: [],
        repos: []
    };
  },
      components: {
      Profile,
      Repos
  },
      computed: {
        orderedRepos: function () {
          return _.orderBy(this.repos, 'stargazers_count', 'desc');
          }
      },
      methods: {
        getUser: function (e) { 
       
          e.preventDefault();   
          var search = document.getElementById("search").value;
          search = search.split(' ').join('')

          const { url, count, client_id, client_secret} = this.github;
          axios.get(
              `${url}/${search}?client_id=${client_id}&client_secret=${client_secret}`
            )
            .then(({ data }) => (this.user = data))
            .catch((e) => {
              console.log('Whoops! Houve um erro.', e.message || e)
              this.errored = true
              this.valorResult = false
            });

          axios.get(
              `${url}/${search}/repos?per_page=${count}&client_id=${client_id}&client_secret=${client_secret}`
            )
            .then(({ data }) => (this.repos = data));
              this.errored = false
              this.valorResult = true
              return this.valor = false 
              
              
        },

        mostrarDiv() {
          return this.valor == true
        },
        mostrarDivResult() {
          return this.valorResult == true
        }
      }
};
</script>