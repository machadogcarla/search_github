  
<template>
  <div>
    <div class="row">
      <div class="col-md-4">
        <div
          class="card"
          style="width: 18rem;"
        >
          <img
            class="card-img-top"
            :src="user.avatar_url"
            alt="Imagem de perfil"
          >
          <ul class="list-group list-group-flush">
            <li class="list-group-item"><h2>{{user.name}}</h2></li>
            <li class="list-group-item">{{user.login}}</li>
            <li class="list-group-item"><span class="material-icons"> work_outline </span>{{user.company}}</li>
            <li class="list-group-item"><span class="material-icons"> place </span>{{user.location}}</li>
            <!--<li class="list-group-item"><span class="material-icons">star_outline</span>{{repo.stargazers_count}}></li>-->
            <li class="list-group-item"><span class="material-icons">inventory_2</span>{{user.public_repos}}</li>
            <li class="list-group-item"><span class="material-icons"> people_outline </span> {{user.followers}}</li>

          </ul>
         
        </div>
      </div>
    </div>
  </div>
</template>

<script>
    export default {
    props: ["user"],
    };

</script>