<template>
    <main class="text-primary">
        <h2>Add an article</h2>
        <br />
        <form @submit.prevent="handleSubmit">
            <label for="title">Article Title: </label>
            <input type="text" name="text" v-model="title" />
            <!-- <div v-show="submitted && !text">Article Title is required</div> -->

            <br /> <br />

            <label for="author">Author name: </label>
            <input type="text" name="text" v-model="author" />
            <!-- <div v-show="submitted && !text">Author name is required</div> -->

            <br /> <br />

            <label for="article_text">Article text: </label>
            <input type="text" name="text" v-model="article_text" />
            <!-- <div v-show="submitted && !text">Article text is required</div> -->

            <br /> <br />

            <button class="btn btn-primary">Add</button>
            <div v-if="error">{{ error }}</div>
        </form>

    </main>

</template>

<script>
import { articleService } from '../../services/article.service';

export default {
    data() {
        return {
            title: "",
            author: "",
            article_text: ""
        };
    },
    methods: {
        handleSubmit(e){
            this.submitted = true
            this.error = ""
            articleService.create(this.title, this.author, this.article_text)
            .then(() => {
                console.log("Article has been posted successfully")
                alert("Article has been posted successfully");  
            })
            .catch(error => this.error = error)
        }
    }
  }
</script>