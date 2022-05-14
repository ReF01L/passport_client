<template>
    <div class="card" @click="$router.push(`/profile/${pk}`)">
        <img :src="image" alt="" class="img">
        <div class="name">{{ name }}</div>
        <div class="lastname">{{ lastname }}</div>
        <div class="user_id">{{ user_id }}</div>
        <div class="nat">{{ nat }}</div>
        <div class="gunlic">{{ gunlic }}</div>
        <div class="crime">{{ crime }}</div>
    </div>
</template>

<script>
export default {
    name: "CardComp",
    props: {
        name: String,
        lastname: String,
        user_id: String,
        nat: String,
        gunlic: String,
        crime: String,
        image: String,
        pk: String
    }
}
</script>

<style lang="sass" scoped>
    .card
        width: 120px
        height: 180px
        display: flex
        flex-direction: column
        justify-content: center
        align-items: center
        border: 1px solid black
        padding: 5px
        margin: 10px
        -webkit-transition: 0.4s
        -moz-transition: 0.4s
        -ms-transition: 0.4s
        -o-transition: 0.4s
        transition: 0.4s
        & .img
            width: 60px
            height: 60px
        &:hover
            cursor: pointer
            -webkit-transform: scale(1.2)
            -moz-transform: scale(1.2)
            -ms-transform: scale(1.2)
            -o-transform: scale(1.2)
            transform: scale(1.2)
</style>