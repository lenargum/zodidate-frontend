<template>
  <div id="app">
<!--    <div id="nav">-->
<!--      <router-link to="/">Home</router-link>-->
<!--      |-->
<!--      <router-link to="/about">About</router-link>-->
<!--      <span v-if="isLoggedIn"> | <a @click="logout">Logout</a></span>-->
<!--    </div>-->
    <router-view/>
  </div>
</template>

<script>
export default {
  computed : {
    isLoggedIn : function(){ return this.$store.getters.isLoggedIn}
  },
  methods: {
    logout: function () {
      this.$store.dispatch('logout')
          .then(() => {
            this.$router.push('/login')
          })
    }
  },
  created: function () {
    this.$http.interceptors.response.use(undefined, function (err) {
      // eslint-disable-next-line no-unused-vars
      return new Promise(function (resolve, reject) {
        if (err.status === 401 && err.config && !err.config.__isRetryRequest) {
          this.$store.dispatch("logout")
        }
        throw err;
      });
    });
  }
}
</script>

<style lang="scss">
@import "~@/scss/_reset.scss";

#app {
  font-family: 'Helvetica', sans-serif;
}

</style>