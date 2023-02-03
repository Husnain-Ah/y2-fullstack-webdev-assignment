<template>
    <main class="text-primary">
        <h2>Rewrite an article</h2>
            <br />
            <form @submit.prevent="handleSubmit">
                <label for="article_id">Article ID: </label>
                <input type="int" name="int" v-model="article_id" />
                <div v-show="submitted && !int">Article ID is required</div>

                <br /> <br />
    
                <label for="title">Article Title: </label>
                <input type="text" name="text" v-model="title" />
                <div v-show="submitted && !text">Article Title is required</div>
    
                <br /> <br />
    
                <label for="author">Author name: </label>
                <input type="text" name="text" v-model="author" />
                <div v-show="submitted && !text">Author name is required</div>
    
                <br /> <br />
    
                <label for="article_text">Article text: </label>
                <input type="text" name="text" v-model="article_text" />
                <div v-show="submitted && !text">Article text is required</div>
    
                <br /> <br />
    
                <button class="btn btn-primary">Append</button>
            </form>

    </main>
  
    </template>
    
    <script>
    import { articleService } from '../../services/article.service';
    
    export default {
        data() {
            return {
                article_id: "",
                title: "",
                author: "",
                article_text: ""
            };
        },
        methods: {
            handleSubmit(e){
                this.submitted = true
                this.error = ""
                articleService.patch(this.article_id, this.title, this.author, this.article_text)
                .then(() => {
                    console.log("Article has been patched successfully")
                    alert("Article has been patched successfully")
                })
                .catch(error => this.error = error)
            }
        }
      }
    </script>