<template>
    <div class = "text-primary text-center text-nowrap ">
        <br />
        <h1 class="font-weight-bold">Login</h1>
        <br />
        <form @submit.prevent="handleSubmit" >
            <div class="form-group">
                <label for="email">Email: </label>
                <input type="email" class="form-control" name="email" v-model="email" />
                <div v-show="submitted && !email">Email is required</div>
                <br /> <br />
            </div>
            
            <div class="form-group"> 
                <label for="password">Password: </label>
                <input type="password" class="form-control" name="password" v-model="password" />
                <div v-show="submitted && !password">Password is required</div>
                <br /> <br />
            </div>
            <!-- <p>{{email + " " + password}}</p> -->

            <button class="btn btn-primary">Login</button>

            <!-- <div v-if="error">{{ error }}</div> -->
        </form>

    </div>
</template>

<script>

import { usersService }  from '../../services/users.service';

export default {
    data(){
        return {
            email: "",
            password: "",
            submitted: false
        }
    },
    methods: {
        handleSubmit(e){
            this.submitted = true
            this.error = ""
            
            console.log("🚀 ~ file: Login.vue:59 ~ handleSubmit ~ email", this.email)
            usersService.login(this.email, this.password)
            .then(result  => { 
            console.log("Auth - go to dash")
            this.$router.push("/dashboard")
            })
            .catch(error => {
                this.error = error;
                this.loading = false;
            })
        }
           
    }
}
</script>

