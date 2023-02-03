<template>
    <div class="text-primary text-center">
      <br />
      <h1>Welcome to my blog!</h1>
      <br />
      <em v-if="loading">Loading articles...</em>

      <ul v-if="articles.length">
        <li v-for="article in articles" :key="article.article_id">
          <router-link :to="'/article/' + article.article_id">
            {{'Id : ' + article.article_id + ' ' + article.title + ' by ' + article.author }}
          </router-link>
        </li>
      </ul>

      <div v-if="error">
          {{ error }}
      </div>

    </div>
</template>

<script>
import { articleService } from '../../services/article.service';

export default {
  data() {
    return {
      articles: [],
      error: "",
      loading: true
    }
  },
  mounted() {
    articleService.getAll()
    .then(articles => {
      console.log("here?", articles)
        this.articles = articles
        this.loading = false
    })
    .catch(error => this.error = error)
  }
}
</script>

