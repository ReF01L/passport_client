<template>
    <main class="main">
        <input type="search" class="search" v-model="search">
        <div class="cards">
            <CardComp v-for="card in searchCards" :key="card.id"
                      :name="card.name"
                      :lastname="card.lastname"
                      :user_id="card.user_id"
                      :nat="card.nat"
                      :gunlic="card.gunlic"
                      :crime="card.crime"
                      :image="card.image"
                      :pk="card.id"
            />
        </div>
    </main>
</template>

<script>
import axios from "axios"
import CardComp from "@/components/CardComp";

export default {
    name: "MainPage",
    components: {CardComp},
    data: () => {
        return {
            cards: [],
            search: ''
        }
    },
    mounted() {
        axios.get(`http://127.0.0.1:8000/api/passports`)
            .then(res => {
                if (res.status === 200) {
                    this.cards = res.data
                }
            })
            .catch(err => {
                alert('Что-то пошло не так:\n' + err)
            })
    },
    computed: {
        searchCards() {
            return this.cards.filter(user => user.name.toLowerCase().includes(this.search.toLowerCase()) ||
                user.lastname.toLowerCase().includes(this.search.toLowerCase()) ||
                user.user_id.toLowerCase().includes(this.search.toLowerCase())
            )
        }
    }
}
</script>

<style lang="sass" scoped>
.search
    margin-left: calc(50% - 180px)
    width: 360px
    height: 35px
    outline: none
    border: 1px solid gray
    margin-top: 25px
    margin-bottom: 10px
    padding: 5px 10px

.cards
    display: flex
    flex-wrap: wrap
    width: 1080px
    margin-left: calc((100vw - 1080px) / 2)

</style>