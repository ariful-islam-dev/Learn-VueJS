<script>
const API_URL = `https://api.github.com/repos/vuejs/core/commits?per_page=3&sha=`;
export default {
  data: ()=>({
    branches: ['main', 'v2-compat'],
    currentBranch: 'main',
    commits:[]
  }),
  created(){
    this.fetchData()
  },
  watch: {
    currentBranch: 'fetchData'
  },
  methods: {
    async fetchData (){
      const url = `${API_URL}/${this.currentBranch}`;
      this.commits = await(await fetch(url)).json();
    },
    truncate (v){
      const newLine = v.indexOf('\n');
      return newLine > 0? v.slice(0, newLine): v
    },
    formateDate(v){
      return v.replace(/T|Z/g, '')
    }
  }
}
</script>
<template>
  <h1>Latest Vue Core Commits</h1>
  <template v-for="branch in branches" v-bind:key="branch">
    <input type="radio" :id="branch" :value="branch" v-model="currentBranch" name="branch" >
    <label for="branch">{{ branch }}</label>
  </template>
  <p>Vuejs/vue@{{ currentBranch }}</p>
  <ul v-if="commits.length > 0">
    <li v-for="{html_url, sha, author, commit} in commits" v-bind:key="sha">
      <a :href="html_url" target="_blank" class="commit">{{ sha.slice(0, 7) }}</a>
      - <span class="message">{{ truncate(commit.message) }}</span>
      <br> by
      <span class="author">
        <a :href="author.html_url" target="_blank">{{ commit.author.name }}</a>
      </span>
      at <span class="date">{{ formateDate(commit.author.date) }}</span>
    </li>
  </ul>
</template>
<style>
a{
  text-decoration: none;
  color: #42b883;
}
li{
  line-height: 1.5rem;
  margin-bottom: 20px;
}
.author, .date{
  font-weight: bold;
}
</style>