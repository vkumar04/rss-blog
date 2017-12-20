<template>
  <div id="app">
    <p v-for="entry in JsonData.feed.entries" :key="entry.title">
      {{entry}}
    </p>
  </div>
</template>

<script>
import parser from 'rss-parser'
export default {
  name: 'app',
  data () {
    return {
      proxyURL: 'https://cors-anywhere.herokuapp.com/',
      feedURL: `https://movement.com/blog/feed/`,
      JsonData: {}
    }
  },
  methods:{
    getrss(){
      parser.parseURL(this.proxyURL+this.feedURL, (err,parsed) => {
        if(err){
          alert('blog url is down')
        }
        else{
          this.JsonData = parsed
        }
      })
    }
  },
  created() {
    this.getrss();
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
