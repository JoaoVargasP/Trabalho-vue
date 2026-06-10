<template>
  <section class="container">
    <div class="topbar">
      <h2>Catálogo</h2>
      <div class="controls">
        <search-bar v-model="query" @search="onSearch" />
        <select v-model="category">
          <option value="">Todas categorias</option>
          <option v-for="c in categories" :key="c" :value="c">{{ c }}</option>
        </select>
      </div>
    </div>

    <div class="grid">
      <card-product
        v-for="p in filtered"
        :key="p.id"
        :product="p"
        @add="openModal"
      />
    </div>

    <modal :visible="modalVisible" @update:visible="modalVisible = $event" @confirm="confirmAdd">
      <template #header>Adicionar ao carrinho</template>
      <p>Deseja adicionar <strong>{{ selected?.name }}</strong> ao carrinho?</p>
    </modal>

    <aside class="cart" v-if="cart.length">
      <h3>Carrinho</h3>
      <ul>
        <li v-for="item in cart" :key="item.id">{{ item.name }} — R$ {{ item.price.toFixed(2) }}</li>
      </ul>
      <p><strong>Total: R$ {{ total.toFixed(2) }}</strong></p>
    </aside>
  </section>
</template>

<script>
import SearchBar from '../components/SearchBar.vue'
import CardProduct from '../components/CardProduct.vue'
import Modal from '../components/Modal.vue'
import { products } from '../data/products.js'
import { ref, computed } from 'vue'

export default {
  name: 'Catalog',
  components: { SearchBar, CardProduct, Modal },
  setup() {
    const all = ref(products)
    const query = ref('')
    const category = ref('')
    const modalVisible = ref(false)
    const selected = ref(null)
    const cart = ref([])

    const categories = computed(() => {
      const set = new Set(all.value.map(p => p.category))
      return Array.from(set)
    })

    const filtered = computed(() => {
      return all.value.filter(p => {
        const matchesQuery = p.name.toLowerCase().includes(query.value.toLowerCase())
        const matchesCategory = category.value ? p.category === category.value : true
        return matchesQuery && matchesCategory
      })
    })

    const openModal = (product) => {
      selected.value = product
      modalVisible.value = true
    }

    const confirmAdd = () => {
      if (selected.value) cart.value.push(selected.value)
      modalVisible.value = false
    }

    const total = computed(() => cart.value.reduce((s, i) => s + i.price, 0))

    const onSearch = (q) => { query.value = q }

    return { query, category, categories, filtered, modalVisible, selected, openModal, confirmAdd, cart, total, onSearch }
  }
}
</script>

<style scoped>
.container { padding:1rem; max-width:1100px; margin:0 auto; display:grid; grid-template-columns: 1fr; gap:1rem; }
.topbar { display:flex; justify-content:space-between; align-items:center; gap:1rem; flex-wrap:wrap; }
.controls { display:flex; gap:0.5rem; align-items:center; }
.grid { display:grid; grid-template-columns:repeat(auto-fit,minmax(220px,1fr)); gap:1rem; }
.cart { margin-top:1rem; padding:1rem; border:1px solid #e2e8f0; border-radius:8px; background:#f7fafc; }
@media(min-width:900px) {
  .container { grid-template-columns: 1fr 320px; }
  .grid { grid-column: 1 / 2; }
  .cart { grid-column: 2 / 3; height:fit-content; }
}
</style>
