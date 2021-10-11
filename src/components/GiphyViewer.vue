<template>
    <div>
        <b-navbar type="dark" variant="dark">
            <b-navbar-brand href="#">Vue GIPHY</b-navbar-brand>
            <div class="search-box">
                <input type="text" v-model="term" v-on:keyup.enter="searchGiphy()" />
                <b-button class="float-end" variant="primary" @click="searchGiphy()">Search</b-button>
                <b-button class="float-end" variant="success" @click="randomGiphy()">Random</b-button>
                <b-button class="float-end" @click="trendingGiphy()">Trending</b-button>
            </div>
        </b-navbar>
        <br>

        <b-card-group columns>
            <b-card bg-variant="dark" v-for="gif in gifs" :key="gif.id" :img-src="gif.images.fixed_width.url"
                :img-alt="gif.title">
                <b-card-text>
                    <a :href="gif.url" text-variant="white" target="_blank">{{ gif.title }}</a>
                </b-card-text>
            </b-card>
        </b-card-group>
    </div>
</template>

<script>
    import axios from 'axios';

    const GIPHY_URL = "http://api.giphy.com/v1/gifs";
    const VUE_APP_GIPHY_API_KEY = process.env.VUE_APP_GIPHY_API_KEY;

    export default {
        name: 'GiphyViewer',
        data() {
            return {
                gifs: [],
                term: ""
            };
        },
        mounted() {
            this.trendingGiphy();
        },
        methods: {
            trendingGiphy() {
                axios.get(`${GIPHY_URL}/trending?api_key=${VUE_APP_GIPHY_API_KEY}`)
                    .then((response) => {
                        console.log(response.data.data)
                        this.gifs = response.data.data
                    })
                    .catch(error => console.log(error))
            },
            searchGiphy() {
                if (!this.term) {
                    alert('Please enter a search term!');
                    return
                }
                axios.get(`${GIPHY_URL}/search?api_key=${VUE_APP_GIPHY_API_KEY}&q=${this.term}`)
                    .then(response => (
                        this.gifs = response.data.data
                    ))
                    .catch(error => console.log(error))

                this.term = "";
            },
            randomGiphy() {
                axios.get(`${GIPHY_URL}/random?api_key=${VUE_APP_GIPHY_API_KEY}`)
                    .then(response => (
                        this.gifs = [response.data.data]
                    ))
                    .catch(error => console.log(error))
            }
        }
    }
</script>

<style>
    a {
        text-decoration: none !important;
    }

    b-navbar {
        margin-bottom: 10px;
    }

    h1 {
        padding-top: 15px;
    }

    .card {
        margin-bottom: 20px;
    }

    .search-box {
        width: 100%;
        margin-bottom: 20px;
        display: inline-flex;
    }


    @media (min-width: 34em) {
        .card-columns {
            -webkit-column-count: 2;
            -moz-column-count: 2;
            column-count: 2;
        }
    }

    @media (min-width: 48em) {
        .card-columns {
            -webkit-column-count: 3;
            -moz-column-count: 3;
            column-count: 3;
        }
    }

    @media (min-width: 62em) {
        .card-columns {
            -webkit-column-count: 4;
            -moz-column-count: 4;
            column-count: 4;
        }
    }

    @media (min-width: 75em) {
        .card-columns {
            -webkit-column-count: 5;
            -moz-column-count: 5;
            column-count: 5;
        }
    }
</style>