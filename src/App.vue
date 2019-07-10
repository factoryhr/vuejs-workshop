<template>
  <div id="app" class="cards-container">
    <Card 
      v-for="(item, key) in items"
      :key="key"
      :data="item"
    />
  </div>
</template>

<script>
import Card from './components/Card.vue'

export default {
  props: {
    query: {
      type: String,
      default: 'vuejs'
    }
  },
  data() {
    return {
      items: [],
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
            )
            return res.json()
        } catch (err) {
            console.error(err)
            throw err
        }
    }
  },
  components: {
    Card
  },
  async mounted() {
    let response = await this.getResponse(this.query);
    this.items = response.items.slice(0, 6);
  },
}
</script>

