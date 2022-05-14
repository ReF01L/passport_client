<template>
    <main class="main">
        <img :src="profile.image" alt="" class="img">
        <div class="content">
            <div class="content_name">{{ profile.name }}</div>
            <div class="content_lastname">{{ profile.lastname }}</div>
            <div class="content_user_id">{{ profile.user_id }}</div>
            <div class="content_nat">{{ profile.nat }}</div>
            <div class="content_gunlic">{{ profile.gunlic }}</div>
            <div class="content_crime">{{ profile.crime }}</div>
        </div>
    </main>
</template>

<script>
import axios from "axios"

export default {
    name: "ProfilePage",
    data: () => {
        return {
            profile: Object
        }
    },
    mounted() {
        axios.get(`http://127.0.0.1:8000/api/passports/${this.$route.params.profile_id}`)
            .then(res => {
                if (res.status === 200) {
                    this.profile = res.data
                }
            })
            .catch(err => {
                alert('Что-то пошло не так:\n' + err)
            })
    }
}
</script>

<style lang="sass" scoped>
.main
    display: flex
    flex-wrap: wrap
    width: 1080px
    margin-left: calc((100vw - 1080px) / 2)
    padding-top: 120px
    & .img
        width: 320px
        min-height: 420px
        border: 1px solid black
        margin-right: 100px
    & .content
        display: flex
        flex-direction: column
        justify-content: flex-start
        align-items: center
        & div
            font-size: 32px
            margin-bottom: 15px
</style>