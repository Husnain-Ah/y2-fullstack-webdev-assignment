<template>
     <div class="text-primary ">
      <br />
      <h1>{{article.title}}</h1>    
      <br />
      <p>{{article.article_text}}</p>
      <br />
      <p>{{article.date_published}}</p>
      <br/>

      <h2>Add a comment</h2>
        <br />
        <form @submit.prevent="handleSubmit">
            <input type="text" name="text" v-model="comment" />

            <br /> <br />

            <button class="btn btn-primary">Add</button>
            <div v-if="error">{{ error }}</div>
        </form>

        <h2>Comments ({{comments.length}})</h2>

        <ul v-if="comments.length">
        <li v-for="comment in comments" :key="comment.comment_id">
          <p >{{'Id : ' + comment.comment_id + ' ' + comment.comment_text + ' ' + comment.date_published}}</p>
          <!-- {{comment.comment_text}} +  {{comment.date_published}} -->
        </li>
      </ul>

        
        <br/>
       

    </div>
</template>

<script>
import { articleService }  from '../../services/article.service';
import { commentsService }  from '../../services/comments.service';

export default {
  data() {
    return {
      article: [],
      comments: [],
      num_comments: null,
      comment: "",
      error: "",
    }
  },
  created() { 
    this.article.loading = true;
    this.comments.loading = true;

    articleService.getOne(this.$route.params.id)
    .then((article) => {
        this.article = article;
        commentsService.getAll(this.$route.params.id)
        .then((comments) => { 
            this.comments = comments
            this.num_comments = comments.length
            
            console.log(this.article);
        })
        .catch(error => this.error = error)
    })
    .catch(error => this.error = error)
  },
  methods: {
    handleSubmit(e){
      this.submitted = true
      this.error = ""
      commentsService.create(this.$route.params.id, this.comment)
      .then(() => {
        commentsService.getAll(this.$route.params.id)
        .then((comments) => { 
            this.comments = comments
            this.num_comments = comments.length
            
            console.log(this.article);
        })
        .catch(error => this.error = error)
      })
    }
  }
}
</script>>

