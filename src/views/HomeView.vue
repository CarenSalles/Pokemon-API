<script setup>
import Pokemon from '@/services/apiPokemon.js';
import { ref, onBeforeMount, reactive } from 'vue';
import CardPokemon from '@/components/CardPokemon.vue';

const service = new Pokemon([]);

let pokemons = ref([]);

onBeforeMount(async()=>{
    pokemons.value = await service.fetchAll();
    poke.value = await service.fetchOnePokemon();
})

let poke = ref([])
// console.log(poke)

</script>

<template>
    <main>
    <header class="header">
        <img class="header__img" src="@/assets/images/pokeapi-logo.png" alt="logo-pokemon">
    </header>

    <form class="filter" action="#">
        <div class="filter__search">
            <label for="search" class="search__title">Nombre o número</label>
            <div class="filter__container-search">
                <input type="text" id="search" class="search__input">
                <button class="search__button"><i class="fa-solid fa-magnifying-glass icon-search"></i></button>
            </div>
        </div>

        <div class="filter__type">
             <label for="type" class="type__title">Búsqueda por tipo</label>
             <select name="type" id="type" class="type__select">
                <option value=""  class="type__option" selected>Seleccione el tipo a filtrar</option>
                 <option value=""  class="type__option">Electrico</option>
                 <option value="" class="type__option">Planta</option>
                 <option value="" class="type__option">Agua</option>
                 <option value="" class="type__option">Fuego</option>
             </select>
        </div>
    </form>
    <div class="container-cards">
        <div class="container-cards__wrap"> 
             <CardPokemon v-for="pokemon in pokemons" :key="pokemon.url" :url="pokemon.url" :name="pokemon.name" /> 
            
        </div> 
    </div>
    <footer class="footer">
        <p class="footer__copy">POKE APaI</p>
    </footer>
</main>
</template>

<style scoped lang="scss">
@use '@/scss/colors' as c;
@use '@/scss/mixins' as m;
@use '@/scss/container-cards' ;
@use '@/scss/filter';

    main{
      @include m.flex(flex, column, nowrap, auto ,center);
        background: rgb(58, 56, 56);
    }

    .header{
        background: rgb(255, 254, 254);
        @include m.flex(flex, auto, nowrap, center , auto );
        width: 60%;
        padding-bottom: 1em;
        &__img{
            width: 30%;
        }
    }

    .footer{
          background: map-get(c.$colors , "dark-blue" );
          @include m.flex(flex, auto, nowrap, center ,center);
          width: 100% ;
          padding: 2em;

          &__copy{
            color:  map-get( c.$colors, "white" );
          }
    }
    
</style>