<template>
    <div class="card mb-4">
        <div class="card-image">
            <figure class="">
                <img :src="currentImg" alt="Placeholder image">
            </figure>
        </div>
        <div class="card-content">
            <div class="media">
                <div class="media-content">
                    <p class="title is-4">{{name}}</p>
                    <p class="subtitle is-6">{{pokemon.type}}</p>
                </div>
            </div>
            <div class="content">
                <button class="button is-medium is-fullwidth" @click="mudarSprite">Mudar sprite</button>
            </div>
        </div>
    </div>
</template>

<script>
import axios from 'axios';

export default {
    created: function () {
        axios.get(this.url).then(result => {
            this.pokemon.type = result?.data?.types[0]?.type?.name
            this.pokemon.front = result?.data?.sprites.front_default
            this.pokemon.back = result?.data?.sprites.back_default
            this.currentImg = this.pokemon.front
    })
    },
    data() {
        return {
            isFront: true,
            currentImg: '',
            pokemon: {}
        }
    },
    props: {
        num: Number,
        name: String,
        url: String
    },
    filters: {
        upper: function (value) { return value[0].toUpperCase() + value.slice(1) }
    },
    methods:{
        mudarSprite: function(){
            this.currentImg = this.isFront ? this.pokemon.back : this.pokemon.front
            this.isFront = !this.isFront
        }
    }
}
</script>

<style>
</style>