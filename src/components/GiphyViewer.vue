<template>
    <div>
        <h1>Vue GIPHY</h1>
        <b-card-group columns>
            <b-card v-for="gif in gifs" :key="gif.id" :img-src="gif.images.fixed_width.url" :img-alt="gif.title"
                bg-variant="dark" class="width">
                <b-card-text>
                    <a :href="gif.url" text-variant="white" target="_blank">{{ gif.title }}</a>
                </b-card-text>
            </b-card>
        </b-card-group>
    </div>
</template>

<script>
    import axios from 'axios';

    const GIPHY_URL = "http://api.giphy.com/v1/gifs/";
    const API_KEY = "moEu06BVp7DM6wixSDc2EJTbOKSmy9N3";

    export default {
        name: 'GiphyViewer',
        data() {
            return {
                gifs: []
            };
        },
        mounted() {
            axios.get(`${GIPHY_URL}trending?api_key=${API_KEY}`)
                .then((response) => {
                    console.log(response.data.data)
                    this.gifs = response.data.data
                })
                .catch(error => console.log(error))
        },
        methods: {

        }
    }
</script>

<style>
    a {
        text-decoration: none !important;
    }

    .card {
        margin-bottom: 20px;
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