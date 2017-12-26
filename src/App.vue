<template>
  <div id="app">
    <h4>{{postID}}</h4>
    <h4>{{latestPost.title.rendered}}</h4>
    <h4>{{latestPost.content.rendered.replace(/<\/?[^>]+>/gi, '')}}</h4>
    <p class="post" v-for="post in jsonData" :key="post.id">
      {{post.id}}
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
      feedURL: 'https://movement.com/blog/wp-json/wp/v2/posts/',
      mediaURL: 'https://movement.com/blog/wp-json/wp/v2/media/',
      jsonData: [],
      latestPost: {},
      postID: null,
    }
  },
  methods:{
    getData(){
      axios.get(this.feedURL)
        .then((response) => {
          this.jsonData = response.data
          this.latestPost = this.jsonData[0]
          this.jsonData.shift()
          for(let i = 0; i < this.jsonData.length; i++){
            this.postID = this.jsonData[i].id
          }
        })
        .catch((error) => {
          console.log(error)
        })
    },
  },
  created() {
    this.getData(),
    this.test()
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
