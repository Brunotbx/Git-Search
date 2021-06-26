<template>
  <div id="App">
    <section class="container-fluid py-5 bg-secondary text-white">
      <div class="container">
        <div class="row text-center justify-content-center py-2">
          <h1 class="display-4">GitHub - Search</h1>
          <p class="lead mb-5">Informe o usuário que deseja buscar</p>

          <form action="" class="col-xl-5 col-9" >
            <div class="input-group mb-3">
              <input
                  v-focus
                  ref="myInput"
                  id="search"
                  type="text"
                  class="form-control"
                  required
                />
              <button class="btn btn-secondary border" @click='getFormValue()'>Buscar</button>
            </div>
          </form>

        </div>
      </div>
    </section>

    <section class="container">
      <div class="row">
        <div class="col-xl-4 col-lg-6" v-if="user.length !== 0">
          <Profile :user="user" />
        </div>
        <div class="col-xl-8 col-lg-6">
          <Repository v-for="repo in repos" :key="repo" :repo="repo" />
        </div>
      </div>
    </section>
  </div>
</template>

<script>
import Profile from "../components/Profile.vue";
import Repository from "../components/Repository.vue";
import axios from "axios";

const focus = {
    inserted: (el) => {
        el.focus()
    }
}

export default {

  name: "Home",

  directives: {
      focus
  },

  data() {
    return {
      github: {
        url: "https://api.github.com/users",
        client_id: "18ec191b0f775ede79b7",
        client_secret: "f669c98dfa86b50e53b41f292668af1aab4b9a5d",
        count: 10,
        sort: "created: asc",
      },
      output: "",
      user: [],
      repos: [],
    };
  },

  components: {
    Profile,
    Repository,
  },

  methods: {
    getFormValue(){
      this.output = this.$refs.myInput.value;
      this.getUser()
    },

    getUser() {
      const user = this.output;
      const { url, client_id, client_secret, count, sort } = this.github;

      axios
        .get(
          `${url}/${user}?client_id=${client_id}&client_secret=${client_secret}`
        )
        .then(({ data }) => (this.user = data));

      axios
        .get(
          `${url}/${user}/repos?per_page=${count}&sort=${sort}&client_id=${client_id}&client_secret=${client_secret}`
        )
        .then(({ data }) => (this.repos = data));
    },
  },
};
</script>
