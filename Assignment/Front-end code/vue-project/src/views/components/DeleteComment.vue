<template>
    <main class="text-primary">
        <h2>Delete a comment</h2>
            <br />
            <form @submit.prevent="handleSubmit">
                <label for="comment_id">Comment ID: </label>
                <input type="int" name="int" v-model="comment_id" />
                <div v-show="submitted && !int">Comment ID is required</div>

                <button class="btn btn-primary">Delete</button>
            </form>

    </main>
   
    </template>
    
    <script>
    import { commentsService }  from '../../services/comments.service';
    
    export default {
        data() {
            return {
                comment_id: ""
            };
        },
        methods: {
            handleSubmit(e){
                this.submitted = true
                this.error = ""
                commentsService.deleteComment(this.comment_id)
                .then(() => {
                    console.log("Comment has been deleted successfully")
                    alert("Comment has been deleted successfully");
                })
                .catch(error => this.error = error)
            }
        }
      }
    </script>