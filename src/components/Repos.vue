
<template>
  <div class="card card-body mb-2">
    <div class="row">
      <div class="col-md-6">
        <p>{{repo.name}}</p>
        <p class="repo">{{repo.description}} </p>
        <p class="repo"><span class="material-icons">star_outline</span> {{repo.stargazers_count}} </p>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: ["repo"]
};
</script>