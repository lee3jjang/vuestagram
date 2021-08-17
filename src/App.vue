<template>
<div class="header">
  <ul class="header-button-left">
    <li>Cancel</li>
  </ul>
  <ul class="header-button-right">
    <li v-if="step==1 | step==0" @click="step++">Next</li>
    <li v-if="step==2" @click="publish">발행</li>
  </ul>
  <img src="./assets/logo.png" class="logo">
</div>

<Container :content="content" :url="url" :게시물들="게시물들" :step="step" @write="this.content=$event" />

<button @click="more">더보기</button>
 
<div class="footer">
  <ul class="footer-button-plus">
    <input @change="upload" type="file" id="file" class="inputfile" />
    <label for="file" class="input-plus">+</label>
  </ul>
</div>

</template>

<script>
import Container from './components/Container.vue';
import postdata from './postdata.json';
import axios from 'axios';

export default {
  name: 'App',
  data() {
    return {
      step: 0,
      클릭수: 0,
      게시물들: postdata,
      url: '',
      content: '',
      선택필터: '',
    }
  },
  components: {
    Container
  },
  methods: {
    more() {
      axios.get(`https://codingapple1.github.io/vue/more${this.클릭수}.json`)
        .then(res => {
          this.게시물들.push(res.data);
          this.클릭수++;
        });
    },
    upload(event) {
      let file = event.target.files[0];
      this.url = URL.createObjectURL(file);
      this.step = 1;
    },
    publish() {
      let 내게시물 = {
        "name": "Kim Hyun",
        "userImage": "https://placeimg.com/100/100/arch",
        "postImage": this.url,
        "likes": 36,
        "date": "May 15",
        "liked": false,
        "content": this.content,
        "filter": this.선택필터,
      };
      this.게시물들.unshift(내게시물);
      this.step = 0;
    },
  },
  mounted() {
    this.emitter.on('fire', (data) => {
      this.선택필터 = data;
    });
  },
}
</script>

<style>
@import 'reset.css';
@import url('https://fonts.googleapis.com/css?family=Poppins:100,200,300,400,500,600,700,800,900');

ul {
  padding: 5px;
  list-style-type: none;
}
.logo {
  width: 22px;
  margin: auto;
  display: block;
  position: absolute;
  left: 0;
  right: 0;
  top: 13px;
}
.header {
  width: 100%;
  height: 40px;
  background: white;
  padding-bottom: 8px;
  position: sticky;
  top: 0;
}
.header-button-left {
  color: skyblue;
  float: left;
  width: 50px;
  padding-left: 20px;
  cursor: pointer;
  margin-top: 15px;
}
.header-button-right {
  color: skyblue;
  float: right;
  width: 50px;
  cursor: pointer;
  margin-top: 15px;
}
.footer {
  width: 100%;
  position: sticky;
  bottom: 0;
  padding-bottom: 10px;
  background: white;
}
.footer-button-plus {
  width: 80px;
  margin: auto;
  text-align: center;
  cursor: pointer;
  font-size: 24px;
  padding-top: 12px;
}
.inputfile {
  display: none;
}
.input-plus {
  cursor: pointer;
}
#app {
  font-family: 'Poppins', sans-serif;
  box-sizing: border-box;
  margin-top: 60px;
  width: 100%;
  min-width: 460px;
  margin: auto;
  position: relative;
  border-right: 1px solid #eee;
  border-left: 1px solid #eee;
}
</style>
