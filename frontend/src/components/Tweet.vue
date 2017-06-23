<template>
  <div class="tweet">
    <div>
      <strong>{{ tweet.auteur.prenom }}</strong>
      <strong>{{ tweet.auteur.nom }}</strong>
      <span class="handle">@{{ tweet.auteur.handle }}</span>
      - {{ moment(tweet.date).fromNow() }}
    </div>
    <div>
      {{ tweet.date }}
      {{ tweet.contenu }}
    </div>
    <div>
      <ul>
        <li class="button"><icon name="reply"/></li>
        <a @click="retweet()">
          <li class="button"><icon name="retweet"/>{{ tweet.retweeters.length }}</li>
        </a>
        <li class="button"><icon name="heart"/></li>
        <li class="button"><icon name="envelope"/></li>
      </ul>
    </div>
  </div>
</template>

<script>
import 'vue-awesome/icons'
import Icon from 'vue-awesome/components/Icon'
import moment from 'moment'
export default {
  name: 'tweet',
  props: ['tweet'],
  components: {Icon},
  created () {
    moment.locale('fr')
  },
  methods: {
    moment: function () {
      return moment()
    },
    retweet: function () {
      this.$http
      .get(
        'http://localhost:8080/retweet',
        {
          responseType: 'text',
          params: {
            utilisateur: 'snoopdog',
            tweet: this.tweet.id
          }
        }
      ).then(response => {
        console.log('retweeté')
      },
      response => {
        // error callback
      })
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
li.button {
 display: inline-block;
}

a {
 color: #42b983;
}

span.handle {
 color: gray;
}
</style>
