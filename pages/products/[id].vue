<template>
  <div class="container grid grid-cols-4 gap-10 py-5">
    <!-- {{ meal.meals }} -->
    <div>
      <img :src="meal.meals[0].strMealThumb" class="rounded-full" alt="" />
    </div>

    <div class="col-span-3">
      <h1 class="text-3xl font-bold pb-2">{{ meal.meals[0].strMeal }}</h1>
      <p>{{ meal.meals[0].strInstructions }}</p>
      <hr class="my-5" />
      <h1 class="font-bold">Watch on YouTube</h1>

      <a :href="meal.meals[0].strYoutube" target="_blank"
        ><i class="fa-brands fa-youtube text-3xl text-red-500"></i
      ></a>
    </div>
  </div>
</template>

<script setup>
const route = useRoute();
const { data: meal } = await useFetch(
  `https://themealdb.com/api/json/v1/1/lookup.php?i=${route.params.id}`
);
</script>

<style lang="scss" scoped>
</style>