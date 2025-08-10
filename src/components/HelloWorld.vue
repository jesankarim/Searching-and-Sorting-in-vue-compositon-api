<template>
  <div>
    <h2>Product List</h2>
    
    <label>
      Search:
      <input v-model="searchTerm" placeholder="Type to search..." />
    </label>
    
    <label>
      Sort by:
      <select v-model="sortBy">
        <option value="name">Name</option>
        <option value="price">Price</option>
      </select>
    </label>

    <ul class="order" v-if="filteredProducts.length>0">
      <li v-for="p in filteredProducts" :key="p.id">
        {{ p.name }} - ${{ p.price }}
      </li>
    </ul>
    <p v-else>No Product Avaliable</p>
  </div>
</template>

<script setup>
import { ref, computed } from 'vue'

const products = ref([
  { id: 1, name: 'Laptop', price: 1200 },
  { id: 2, name: 'mouse', price: 20 },
  { id: 3, name: 'keyboard', price: 50 },
  { id: 4, name: 'monitor', price: 300 }
])

const searchTerm = ref('')  
const sortBy = ref('name')


const filteredProducts = computed(() => {
  
  let result=products.value.filter((p)=>{
    return p.name.toLocaleLowerCase().includes(searchTerm.value.toLocaleLowerCase())
  })
 
  if (sortBy.value === 'name') {
    result.sort((a, b) => a.name.localeCompare(b.name))
  } else if (sortBy.value === 'price') {
    result.sort((a, b) => a.price - b.price)
  }

  return result
})
</script>

<style scoped>
.order li{
  list-style: none;
}

</style>
