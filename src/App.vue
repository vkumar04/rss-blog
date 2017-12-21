<template>
  <div id="app">
    <p v-for="post in jsonData.data" :key="post.id">
      {{post.title.rendered}}

      </br>
      {{post.content.rendered.replace(/<\/?[^>]+>/gi, '') }}
    </p>
  </div>
</template>

<script>
import axios from 'axios'
export default {
  name: 'app',
  data () {
    return {
      feedURL: `https://movement.com/blog/wp-json/wp/v2/posts/`,
      jsonData: {},
      latestPost: {},
      posts: {}
    }
  },
  methods:{
    getData(){
      axios.get(this.feedURL)
        .then((response) => {
          this.jsonData = response
          this.latestPost = this.jsonData
          
        })
        .catch((error) => {
          console.log(error)
        })
    }
  },
  created() {
    this.getData()
  }
}
</script>

<style lang="scss">
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

h1, h2 {
  font-weight: normal;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  display: inline-block;
  margin: 0 10px;
}

a {
  color: #42b983;
}
</style>
