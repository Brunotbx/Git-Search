<!-- Componente para criação do card do Profile do usuário buscado -->

<template>
  <div>
    <div class="card card-body mt-3" style="style=width: 20rem">
      <img :src="user.avatar_url" alt="" class="card-img-top" />

      <ul class="list-group list-group-flush mb-3">
        <li class="list-group-item">
          Repositório:
          <span class="badge bg-secondary">{{ user.public_repos }}</span>
        </li>
        <li class="list-group-item">
          Seguidores:
          <span class="badge bg-secondary">{{ user.followers }}</span>
        </li>
        <li class="list-group-item">
          Seguindo:
          <span class="badge bg-secondary">{{ user.following }}</span>
        </li>
      </ul>

      <div class="card">
        <a :href="user.html_url" class="btn btn-secondary btn-block"
          >Ver Perfil</a
        >
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: ["user"],
};
</script>
