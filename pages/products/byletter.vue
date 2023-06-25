<template>
  <div class="py-5 container">
    <div class="loading" v-if="pending">
      <img src="~/assets/images/loading.gif" alt="" />
    </div>
    <div class="my-2" v-else>
      <label for="">Search Items by First Letter</label>
      <input type="text" v-model="ch" class="border py-2 mx-2" maxlength="1" />
      <button @click="getUrl(ch)" class="py-2 px-10 bg-blue-400 text-white">
        Search
      </button>

      <div class="row g-4">
        <div class="col-md-3" v-for="(p, index) in items.meals" :key="index">
          <NuxtLink :to="`/products/${p.idMeal}`"
            ><ProductCard :product="p"
          /></NuxtLink>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
const ch = ref("a");
const url = ref("https://www.themealdb.com/api/json/v1/1/search.php?f=a");
const { data: items, pending } = await useFetch(url, { refetch: true });

function getUrl(ch) {
  url.value = `https://www.themealdb.com/api/json/v1/1/search.php?f=${ch}`;
}
</script>

<style scoped>
</style>