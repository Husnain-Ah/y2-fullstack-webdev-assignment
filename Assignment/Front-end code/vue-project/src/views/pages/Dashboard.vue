<template>
        <div class="text-primary">
        <h1>Dashboard</h1>
        <form @submit.prevent="handleSubmit">
            <button class="btn btn-primary">Logout</button>
            <div v-if="error">{{ error }}</div>
        </form>
        </div>
        <br />
        <PostUser/>
        <br />
        <GetUsers/>
        <br />
        <PostArticle/>
        <br />
        <DeleteArticle/>
        <br />
        <PatchArticle />
        <br />
        <DeleteComment />
    
</template>

<script>
import { usersService }  from '../../services/users.service';

import GetUsers from '../components/GetUsers.vue';
import PostUser from '../components/PostUser.vue';
import PostArticle from '../components/PostArticle.vue';
import DeleteArticle from '../components/DeleteArticle.vue';
import PatchArticle from '../components/PatchArticle.vue';
import DeleteComment from '../components/DeleteComment.vue';


export default {
    data() {
        return {
            submitted: false
        };
    },
    methods: {
        handleSubmit(e) {
            this.submitted = true;
            this.error = "";
            usersService.logout()
                .then(result => {
                alert("Logged out successfully")
                console.log("Logged out - go to homepage");
                this.$router.push("/");
            })
                .catch(error => {
                this.error = error;
                this.loading = false;
            });
        }
    },
    components: {
    GetUsers,
    PostUser,
    PostArticle,
    DeleteArticle,
    PatchArticle,
    DeleteComment,
    }
}
</script>

