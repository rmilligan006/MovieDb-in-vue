<template>
<div class="movie-details">
 <img :src="movie.Poster" alt="Movie Poster"  class="featured-img"/>
 <h2 class="title">{{movie.Title}}</h2>
 <h2 class="imdbRating">imdb: {{movie.imdbRating}}</h2>
 <p class="year">{{movie.Year}}</p>
 <p class="rating">Rated: {{movie.Rated}}</p>
 <p class="genre">Genre: {{movie.Genre}}</p>
 <p class="actors">Actors: {{movie.Actors}}</p>
 <p class="director">Director: {{movie.Director}}</p>
 <p class="plot">Plot: {{movie.Plot}}</p>
</div>
</template>

<script>
import {ref, onBeforeMount } from 'vue';
import {useRoute} from 'vue-router';
import env from '@/env.js'

export default {
setup () {
    const movie = ref({});
    const route = useRoute();

    onBeforeMount(() => {
             fetch(`http://www.omdbapi.com/?apikey=${env.apikey}&i=${route.params.id}&plot=full`)
        .then(response => response.json())
        .then(data => {
            movie.value = data;
            
        });
    });
    return {
        movie,
        
    }
}
}
</script>

<style lang="scss">
.movie-details {
    padding: 16px;
    
    h2 {
    color: #fff;
    font-size: 20px;
    font-weight: 600;
    margin-bottom: 16px;
    text-align: center;    
    }

    .featured-img {
        display: block;
        max-width: 200px;
        margin-bottom: 16px;
        
    }

    p {
        color: #fff;
        line-height: 1.4;
        font-size: 18px;
        margin-bottom: 10px;
    }
}
</style>