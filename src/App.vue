<template>
  <div>
    <div class="container">
            
      <div class="search card card-body">
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

      <div
        class="row mt-3"
        v-if="user.length !== 0"
      >
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
      github: {
        url: "https://api.github.com/users",
        //client_id: "3101ae14397bfa4010a2d",
        //client_secret: "46fa1f407bc140a181b2f013bab033b954e23a18",
        count: "10",
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
    
    const { url, count} = this.github;
      axios.get(
          `${url}/${search}`
        )
        .then(({ data }) => (this.user = data));

        axios
        .get(
          `${url}/${search}/repos?per_page=${count}`
        )
        .then(({ data }) => (this.repos = data));
      
  }
  }
 
};
</script>