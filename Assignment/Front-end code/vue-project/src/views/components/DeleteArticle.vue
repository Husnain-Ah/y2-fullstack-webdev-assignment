<template>
    <main class="text-primary">
        <h2>Delete an article</h2>
            <br />
            <form @submit.prevent="handleSubmit">
                <label for="article_id">Article ID: </label>
                <input type="int" name="int" v-model="article_id" />
                <div v-show="submitted && !int">Article ID is required</div>

                <button class="btn btn-primary">Delete</button>
            </form>

    </main>
   
    </template>
    
    <script>
    import { articleService } from '../../services/article.service';
    
    export default {
        data() {
            return {
                article_id: ""
            };
        },
        methods: {
            handleSubmit(e){
                this.submitted = true
                this.error = ""
                articleService.deleteArticle(this.article_id)
                .then(() => {
                    console.log("Article has been deleted successfully")
                    alert("Article has been deleted successfully");
                })
                .catch(error => this.error = error)
            }
        }
      }
    </script>