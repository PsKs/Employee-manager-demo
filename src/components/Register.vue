<template>
    <div class="container">
        <div class="row">
            <div class="col s12 m8 offset-m2">
                <div class="login card-panel grey lighten-4 black-text center">
                <h3>Register</h3>
                <form>
                    <div class="input-field">
                        <i class="material-icons prefix">email</i>
                        <input type="email" id="email" v-model="email">
                        <label class="black-text" for="email">Email Address</label>
                    </div>
                    <div class="input-field">
                        <i class="material-icons prefix">lock</i>
                        <input type="password" id="password" v-model="password">
                        <label class="black-text" for="password">Password</label>
                    </div>
                    <button @click.prevent="register" class="btn btn-large btn-extended grey lighten-4 black-text">Register</button>
                </form>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
import firebase from 'firebase'

export default {
    name: 'register',
    data() {
        return {
            email: '',
            password: ''
        }
    },
    methods: {
        register() {
            firebase.auth().createUserWithEmailAndPassword(this.email, this.password).then(
                user => {
                    // console.log(user);
                    alert(`Account Created for ${user.email}`);
                    this.$router.go({ path: this.$router.path });
                },
                err => {
                    alert(err.message)
                }
            )
        }
    }
}
</script>