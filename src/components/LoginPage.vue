<template>
    <main class="login">
        <div class="error" v-if="error">Неверный логин или пароль</div>
        <div class="login_input">
            <div class="login_input-title">Логин</div>
            <input type="text" class="login_input-input" v-model="user.login">
        </div>
        <div class="login_input">
            <div class="login_input-title">Пароль</div>
            <input type="password" class="login_input-input" v-model="user.password">
        </div>
        <div class="login-btn" @click="login">Авторизоваться</div>
    </main>
</template>

<script>
import axios from "axios"

export default {
    name: "LoginPage",
    data() {
        return {
            user: {
                login: '',
                password: ''
            },
            error: false
        }
    },
    methods: {
        login() {
            axios.post('http://127.0.0.1:8000/api/login', {
                login: this.user.login,
                password: this.user.password
            })
            .then(res => {
                localStorage.setItem('user_id', res.data.user_id)
                this.$router.replace('/')
            })
            .catch(() => {
                this.error = true
            })
        }
    },
    mounted() {
        if (localStorage.getItem('user_id') !== null) {
            this.$router.replace('/')
        }
    }
}
</script>

<style lang="sass" scoped>
.login
    display: flex
    background-color: #7f8fa6
    min-height: 100vh
    max-width: 100vw
    justify-content: center
    align-items: center
    flex-direction: column
    padding-bottom: 100px
    & .error
        font-size: 22px
        color: #c0392b
    &_input
        margin-top: 15px
        &-title
            margin-bottom: 5px
            margin-left: 3px
            font-size: 22px
        &-input
            width: 720px
            height: 60px
            outline: none
            border: 1px solid gray
            padding: 5px 10px
            margin-right: 25px
            border-radius: 10px
            color: #2f3640
            font-weight: 600
            font-size: 20px
            @media screen and (max-width: 600px)
                width: 180px
                margin-right: 0
                margin-bottom: 10px
    &-btn
        text-transform: capitalize
        height: 50px
        width: 220px
        border-radius: 10px
        padding: 10px
        color: #192a56
        font-size: 22px
        display: flex
        justify-content: center
        align-items: center
        border: 1px solid #192a56
        margin-top: 15px

        &:hover
            cursor: pointer

</style>