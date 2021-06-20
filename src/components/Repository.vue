<!-- Componente para criação do campo de exibição dos repositórios -->

<template>
  <div class="card card-body mt-3">
    <div class="row">
      <div class="h5 mb-2 text-uppercase">
        <a :href="repo.html_url" target="_blank" class="text-decoration-none">{{
          repo.name
        }}</a>
      </div>

      <div class="col-12 mb-3">
        <span class="h6">Descrição: {{ repo.description }}</span>
      </div>

      <div class="col-md-6">
        <span class="badge bg-secondary me-1"
          >Main Language: {{ repo.language }}</span
        >
        <span class="badge bg-warning stars"
          >Stars: {{ repo.stargazers_count }}</span
        >
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: ["repo"],
};
</script>
