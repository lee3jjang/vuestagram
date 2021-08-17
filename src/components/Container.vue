<template>

<div v-if="step==0">
  <Post :게시물="게시물" v-for="게시물 in 게시물들" :key="게시물" />
</div>

<div v-if="step==1">
  <div :class="선택필터" class="upload-image" :style="{ backgroundImage: `url(${url})` }"></div>
  <div class="filters">
    <FilterBox v-for="필터 in 필터들" :key="필터" :url="url" :필터="필터">
      <span>{{필터}}</span>
    </FilterBox>
  </div>
</div>

<div v-if="step==2">
  <div :class="선택필터" class="upload-image" :style="{ backgroundImage: `url(${url})` }"></div>
  <div class="write">
    <textarea @input="$emit('write', $event.target.value)" class="write-box">write!</textarea>
  </div>
</div>

</template>

<script>
import Post from './Post.vue';
import FilterBox from './FilterBox.vue';

export default {
  name: 'Container',
  data() {
    return {
      필터들: ["aden", "_1977", "brannan", "brooklyn", "clarendon", "earlybird", "gingham", "hudson", 
        "inkwell", "kelvin", "lark", "lofi", "maven", "mayfair", "moon", "nashville", "perpetua", 
        "reyes", "rise", "slumber", "stinson", "toaster", "valencia", "walden", "willow", "xpro2"],
    }
  },
  props: {
    게시물들: Array,
    step: Number,
    url: String,
    content: String,
    선택필터: String,
  },
  components: {
    Post,
    FilterBox,
  },
}
</script>

<style>
.upload-image {
  width: 100%;
  height: 450px;
  background: cornflowerblue;
  background-size: cover;
}
.filters {
  overflow-x: scroll;
  white-space: nowrap;
}
.filters::-webkit-scrollbar {
  height: 5px;
}
.filters::-webkit-scrollbar-thumb {
  background: #888; 
  border-radius: 5px;
}
.filters::-webkit-scrollbar-thumb:hover {
  background: #555;
}
.write-box {
  border: none;
  width: 90%;
  height: 100px;
  padding: 15px;
  margin: auto;
  display: block;
  outline: none;
}
</style>