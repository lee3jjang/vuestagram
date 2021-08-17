<template>

<div @click="fire" :class="[필터, 'filter-item']" :style="{ backgroundImage: `url(${url})` }">
  <slot></slot>
</div>

</template>

<script>
export default {
  name: 'FilterBox',
  props: {
    url: String,
    필터: String,
  },
  methods: {
    fire() {
      this.emitter.emit('fire', this.필터);
    }
  }
}
</script>

<style>
.filter-item {
  width: 100px;
  height: 100px;
  margin: 10px 10px 10px auto;
  padding: 8px;
  display: inline-block;
  color: white;
  background-size: cover;
  background-position: center;
  cursor: pointer;
}
</style>