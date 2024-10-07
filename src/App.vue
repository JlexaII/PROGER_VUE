<template>
    <input type="text" v-model="userName" placeholder="Name">
    <input type="password" v-model="userPass" placeholder="Password">
    <input type="email" v-model="userEmail" placeholder="email">

    <button @click="sendData()">Sending...</button>
    <p className="error">{{ error }}</p> 

    <div v-if="users.length == 0" className="user">
        User not found
    </div>

    <div v-else-if="users.length == 1" className="user">
        User one found
    </div>
    <div v-else className="user">
        User more one element found
    </div>
    
    <user v-for="(el, index) in users" :key="index" :user="el" :index="index" :deleteUser="deleteUser" />
      

</template>

<script>
import User from './components/user.vue';

export default {
    components: { User }, 
    data() {
        return {
            users: [],
            error: '',
            userName: '',
            userPass: '',
            userEmail: ''
        }
    },
    methods: {
        sendData() {
            if(this.userName == '') {
                this.error = 'Name not found';
                return;
            } else if(this.userEmail == '') {
                this.error = 'Email not found';
                return;
            } else if(this.userPass == '') {
                this.error = 'Password not found';
                return;
            }

            this.error = '';

            this.users.push({
                name: this.userName,
                pass: this.userPass,
                email: this.userEmail
            })
        },
        deleteUser(index) {
            this.users.splice(index, 1);
        }
    }
}
</script>

<style scoped>
input {
    display: block;
    margin-bottom: 10px;
    border-radius: 3px;
    border: 1px solid silver;
    outline: none;
    padding: 10px 15px;
    background: white;
    color: rgb(43, 33, 33);
}

button {
    border: 0;
    border-radius: 5px;
    outline: none;
    padding: 10px 15px;
    background: rgb(82, 152, 82);
    color: rgb(3, 51, 3);
    cursor: pointer;
    font-weight: bold;
    transition: transform 500ms ease;
}

button:hover {
    transform: translateY(-5px);
}

.user {
    width: 500px;
    margin-top: 20px;
    border: 1px solid silver;
    background: white;
    color: black;
    padding: 20px;
    border-radius: 5px;
}
</style>
