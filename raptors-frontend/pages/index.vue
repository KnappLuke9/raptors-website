<template>
  <div>
    <Nav />
    <div class="container">
      <h1>Welcome to the Raptors floorball team</h1>
      <NuxtLink to="/articles">View news!</NuxtLink>
    </div>
    <div class="container">
    <div v-if="error">
      {{ error }}
    </div>
    <ul v-else>
      <li v-for="article in articles" :key="article.id">
        {{ article.attributes.Title }}
      </li>
    </ul>
    <article-card 
      v-for="article in articles" 
      :key="article.id" 
      :article="article" 
    />
  </div>
  </div>
</template>

<script>
import axios from 'axios'

export default {
  name: 'App',
  data () {
    return {
      articles: [],
      error: null,
    }
  },
  async mounted () {
    try {
      const response = await axios.get('http://localhost:1337/api/articles?populate=*')
      this.articles = response.data.data //fkn really... had to do data.data... fuck this shiiiiiiiiiiiit.. this took me forever to figure out

      console.log(this.articles)
    } catch (error) {
      this.error = error;
    }
  }
}
</script>

<style scoped>
.container {
  text-align: center;
  margin-top: 5rem;
}
</style>

