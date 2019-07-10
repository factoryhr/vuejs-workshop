<template>
  <div @click="flipCard" class="flip-card" :class="{flipped: flipped}">
    <div class="flip-card-inner">
      <div class="flip-card-front">
        <img :src="data.owner.avatar_url" alt="Avatar" style="width:300px;height:300px;">
      </div>
      <div class="flip-card-back">
        <p>{{data.name}}</p> 
        <a :href="data.clone_url" target="_blank">repo</a> 
        <p>{{data.owner.login}}</p>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    data: {
      type: Object,
      default: () => {}
    }
  },
  data() {
    return {
      flipped: false,
    }
  },
  methods: {
    flipCard() {
      this.flipped = !this.flipped;
    }
  },
}
</script>
