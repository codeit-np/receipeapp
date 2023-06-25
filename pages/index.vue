<template>
  <div>
    <section class="loading" v-if="pending">
      <img src="~/assets/images/loading.gif" width="250" alt="" />
    </section>

    <section v-else>
      <div class="container">
        <div class="mb-3">
          <label for="" class="form-label">Select Category</label>
          <select
            class="form-select form-select-lg"
            v-model="name"
            @change="getUrl(name)"
          >
            <option selected>Select one</option>
            <option
              :value="c.strCategory"
              v-for="(c, index) in categoryData.categories"
              :key="index"
            >
              {{ c.strCategory }}
            </option>
          </select>
        </div>
        <div class="row g-4">
          <div class="col-md-3" v-for="(p, index) in data.meals" :key="index">
            <NuxtLink :to="`products/${p.idMeal}`"
              ><ProductCard :product="p"
            /></NuxtLink>
          </div>
        </div>
      </div>
    </section>
  </div>
</template>

<script setup>
let name = ref("Seafood");
const url = ref(`https://www.themealdb.com/api/json/v1/1/filter.php?c=Seafood`);

// Get All Categories
const { data: categoryData } = await useFetch(
  "https://www.themealdb.com/api/json/v1/1/categories.php"
);

const { data, pending } = useFetch(url, { refetch: true });

function getUrl(category) {
  url.value = `https://www.themealdb.com/api/json/v1/1/filter.php?c=${category}`;
}
</script>

<style>
.loading {
  width: 100%;
  height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
}
</style>