<template>
    <main class="text-primary">
        <div class="user-container">
        <p>User List</p>
        <em v-if="loading">Loading users...</em>
    <div class="user-body">
    </div>
    <ul v-if="users.length">
        <li v-for="user in users" :key="user.user_id">
            {{ 'Id : ' + user.user_id + ' First name : ' + user.first_name + ' Last name : ' + user.last_name + ' Email : ' + user.email }}
          
        </li>
      </ul>

      <div v-if="error">
          {{ error }}
      </div>
    </div>

    </main>
    
</template>

<script>
import { usersService }  from '../../services/users.service';

    export default {
        data() {
            return {
                users : [],
                user_id: "",
                first_name: "",
                last_name: "",
                email: "",
                loading: true
            }
  },
  mounted() { 
    usersService.getAll()
    .then((users) => { 
        this.users = users;
        console.log("here?", users)
        this.loading = false
    })
    .catch(error => this.error = error) 
    }   
}
</script>