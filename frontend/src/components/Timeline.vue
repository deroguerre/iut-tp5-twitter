<template>
  <div class="timeline">
    <h1>{{ msg }}</h1>
    <feed :tweets="tweets" :loading="isLoading"/>
  </div>
</template>

<script>
import Feed from './Feed'
import Vue from 'vue'
import Resource from 'vue-resource'
Vue.use(Resource)
export default {
  name: 'timeline',
  data () {
    return {
      tweets: [],
      isLoading: true,
      msg: 'salut'
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
      },
      response => {
        // error callback
      })
    }
  },
  components: { Feed }
}

</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>
