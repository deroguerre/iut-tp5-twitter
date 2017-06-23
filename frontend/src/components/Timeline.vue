<template>
  <div class="timeline">
    <img src='../assets/nerd-dance.jpg'>
    <h1>{{ msg }}</h1>
    <utilisateurs></utilisateurs>
    <feed :tweets="tweets" :loading="isLoading"/>
  </div>
</template>

<script>
import Feed from './Feed'
import Vue from 'vue'
import Resource from 'vue-resource'
import Utilisateurs from './Utilisateurs'
Vue.use(Resource)
export default {
  name: 'timeline',
  data () {
    return {
      tweets: [],
      isLoading: true,
      msg: 'TimeLine'
    }
  },
  created () {
    this.fetchTweets()
  },
  methods: {
    fetchTweets: function () {
      // GET /someUrl
      this.$http.get('http://localhost:8080/list').then(response => {
        // get body data
        this.tweets = response.body
        this.isLoading = false
        this.$emit('retweeted', this.tweet.id)
      },
      response => {
        // error callback
      })
    }
  },
  components: { Feed, Utilisateurs }
}

</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>
