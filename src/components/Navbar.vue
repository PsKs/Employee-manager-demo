<template>
    <nav>
        <div class="nav-wrapper green">
            <div class="container">
                <router-link to="/" class="brand-logo">Employee Manager</router-link>
                <ul class="right">
                    <li v-if="isLoggedin">
                        <span class="email black-text">
                            {{ currentUser }}
                        </span>
                    </li>
                    <li v-if="isLoggedin">
                        <router-link to="/">Dashboad</router-link>
                    </li>
                    <li v-if="!isLoggedin">
                        <router-link to="/login">Login</router-link>
                    </li>
                    <li v-if="!isLoggedin">
                        <router-link to="/register">Register</router-link>
                    </li>
                    <li v-if="isLoggedin">
                        <button @click="logout" class="btn black">Logout</button>
                    </li>
                </ul>
            </div>
        </div>
    </nav>
</template>

<script>
import firebase from 'firebase'

export default {
    name: 'navbar',
    data() {
        return {
            isLoggedin: false,
            currentUser: false,
        }
    },
    created() {
        if (firebase.auth().currentUser) {
            this.isLoggedin = true;
            this.currentUser = firebase.auth().currentUser.email;
        }
    },
    methods: {
        logout() {
            firebase.auth().signOut().then(
                () => {
                    this.$router.go({ path: this.$router.path });
                }
            )
        }
    }
}
</script>
