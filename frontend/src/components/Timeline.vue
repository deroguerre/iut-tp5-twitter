<template>
  <div class="tweet">
    <h1>{{ msg }}</h1>
    <ul>
      <li v-for="tweet in tweets"><tweet :tweet="tweet"/></li>
    </ul>
  </div>
</template>

<script>
import Tweet from './Tweet'
import Vue from 'vue'
import Resource from 'vue-resource'
Vue.use(Resource)
export default {
  name: 'timeline',
  data () {
    return {
      tweets: [
        {
          'auteur': 'Bingo',
          'contenu': 'salut !'
        },
        {
          'auteur': 'MrJoe',
          'contenu': 'hi'
        }
      ]
    }
  },
  components: {Tweet}
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1, h2 {
  font-weight: normal;
}
ul {
 list-style-type: none;
 padding: 0;
}
li {
 display: block;
 margin: 0 10px;
}
</style>
