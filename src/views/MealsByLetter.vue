<template>
  <div class="p-8 bp-0">
    <h1 class="text-4xl font-bold mb-4 text-orange-500">Meals by Letter</h1>
  </div>
  <div class="flex justify-center gap-3 mt-px-8">
    <router-link :to="{name: 'byLetter', params: {letter}}"  
      v-for="letter of letters" 
      :key='letter'
      class="hover:text-orange-500 transition-colors"
      >
        {{ letter }}
    </router-link>
  </div>
  <Meals :meals="meals"></Meals>
</template>

<script setup>
import { computed, onMounted, watch } from 'vue';
import store from '../store';
import { useRoute } from 'vue-router';
import Meals from '../components/Meals.vue';

const route = useRoute()
const letters = 'ABCDEFGHIJKLMNOPQRSTUVWXYZ'.split("")
const meals = computed(() => store.state.mealsByLetter)

watch(route, () => {
  store.dispatch('searchMealsByLetter', route.params.letter)

})      

onMounted(() => {
  store.dispatch('searchMealsByLetter', route.params.letter)
})

</script>