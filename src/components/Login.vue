<template>
  <div class="loginHeader">
    <p v-if="$store.state.loggedIn">Logged in as: <b>{{ $store.state.member.fullName }}</b></p>
    <button v-else v-on:click="loginTrello">Login to Trello</button>
  </div>
</template>

<script>
export default {
  name: 'Login',
  
  methods: {
  
    authenticationSuccess: function() {
      console.log('Authenticated!');
      this.$store.commit('changeLoginStatus', 1)
      this.$store.dispatch('loadMemberData')   
    },

    authenticationFailure: function() {
      console.log('Authentication error!');
      this.$store.commit('changeLoginStatus', 0)
    },

    loginTrello: function () {
      window.Trello.authorize({
        type: 'popup',
        name: 'Trello reporting tool',
        scope: {
          read: 'true',
          write: 'true' },
        expiration: 'never',
        success: this.authenticationSuccess,
        error: this.authenticationFailure
      });
    }



  }
}


</script>

