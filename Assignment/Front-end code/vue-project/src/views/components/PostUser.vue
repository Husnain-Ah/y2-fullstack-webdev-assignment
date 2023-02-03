<template>
    <main class="text-primary">
        <div>
        <h1>Create a new user</h1>
        <form @submit.prevent="handleSubmit">
            <label for="first_name">First name: </label>
            <input type="text" name="text" v-model="first_name" />
            <!-- <div v-show="submitted && !text">First name is required</div> -->

            <br /> <br />

            <label for="last_name">Last name: </label>
            <input type="text" name="text" v-model="last_name" />
            <!-- <div v-show="submitted && !text">Last name is required</div> -->

            <br /> <br />
            
            <label for="email">Email: </label>
            <input type="email" name="email" v-model="email" />
            <div v-show="submitted && !email">Email is required</div>

            <br /> <br />

            <label for="password">Password: </label>
            <input type="password" name="password" v-model="password" />
            <div v-show="submitted && !password">Password is required</div>

            <br /> <br />
            <!-- <p>{{first_name + " " + last_name + " " + email + " " + password}}</p> -->

            <button class="btn btn-primary">Create user</button>
        </form>

    </div>

    </main>
    
</template>

<script>
import { usersService }  from '../../services/users.service';

export default {
    data(){
        return {
            first_name: "",
            last_name: "",
            email: "",
            password: "",
            submitted: false
        }
    },
    methods: {
        handleSubmit(e){
            this.submitted = true
            this.error = "error"
            // const {email, password} = this
            // if(!(email && password)){
            //     return;
            // }

            // if(!(EmailValidator.validate(email))){
            //     this.error = "Email must be a valid email."
            //     return;
            // }

            // const password_pattern = /^(?=.*[A-Za-z])(?=.*\d)[A-Za-z\d]{8,}$/
            // if(!(password_pattern.test(password))){
            //     this.error = "Password not strong enough."
            //     return; 
            // }
            // alert("Button clicked")

            usersService.post(this.first_name, this.last_name, this.email, this.password)
            .then(()  => { 
            console.log("User has been posted successfully")
            alert("User has been posted successfully");

                //need to refresh list of users after posting a user

                // usersService.getAll()
                //     .then((users) => { 
                //     this.users = users;
                //     console.log("here?", users)
                //     })
                //     .catch(error => this.error = error) 
                })
                 .catch(error => {
                    this.error = error;
                    this.loading = false;
                })
        }
    }
   
}
</script>