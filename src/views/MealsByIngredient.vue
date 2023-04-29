<template>
  <Meals :meals="meals"></Meals>
</template>

<script setup>
import Meals from '../components/Meals.vue'
import { onMounted, ref, computed } from 'vue';
import store from '../store';
import { useRoute } from 'vue-router';

const route = useRoute()
const meals = computed(() => store.state.mealsByIngredient)

onMounted(() => {
  store.dispatch('searchMealsByIngredient', route.params.ingredient)
})
 

</script>