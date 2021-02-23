
<template>
  <div class="card card-body mb-2">
    <div class="row">
      <div class="col-md-6">
        <a
          :href="repo.html_url"
          target="_blank"
        >{{repo.name}}</a>
        <p>{{repo.description}} </p>
        <p><span class="material-icons">star_outline</span> {{repo.stargazers_count}} </p>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: ["repo"]
};
</script>