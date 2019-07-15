<template>
  <div id="app">
    <div>
        Pretraži GitHub:
        <input type="text" v-model.lazy="query" @keyup.enter="getResponse(query)">
    </div>

    <div class="cards-container">
      <Card 
        v-for="(item, key) in items"
        :key="key"
        :data="item"
      />
    </div>
  </div>
</template>

<script>
import Card from './components/Card.vue'

export default {
  props: {
    
},
  data() {
    return {
      items: [],
      query: 'VueJS'
    }
  },
  methods: {
    async getResponse (query) {
       try {
            const res = await fetch(
              `https://api.github.com/search/repositories?q=${query}`,
              {
                mode: 'cors'
              }
            ).then(function(response) {
              return response.json()
            })

            this.items = res.items.slice(0, 10);
            return res
        } catch (err) {
            console.error(err)
            throw err
        }
    },
  },
  components: {
    Card,
  },
  async mounted() {
    let response = await this.getResponse(this.query);
//    this.items = response.items.slice(0, 10);
  },
}
</script>

