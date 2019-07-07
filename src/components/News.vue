<template>
  <div class="news">
    <h1>Hacker News</h1>
    <div class="columns medium-3" v-for="(result, index) in results" :key="index">
      <div class="card">
        <div class="card-divider">{{ result.title }}</div>
        <div class="card-section">
          <p>{{ result.url }}.</p>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";

const HNBaseURL = "https://hacker-news.firebaseio.com/v0/";
function buildUrl(url) {
  return HNBaseURL + url + ".json";
}

export default {
  name: "News",
  data() {
    return {
      results: []
    };
  },
  mounted() {
    this.getPosts();
  },
  methods: {
    getPosts() {
      let topstories = buildUrl("topstories");
      axios.get(topstories).then(response => {
        let ids = response.data;
        ids.slice(0, 10).filter(id => {
          let item = buildUrl("item/" + id);
          axios.get(item).then(response => {
            let post = response.data;
            this.results.push({
              title: post.title,
              url: post.url
            });
          });
        });
      });
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
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
