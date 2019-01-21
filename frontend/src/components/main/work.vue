<template>
  <div class="text-center spacer" id="work">
    <b-container>
      <h2>Works</h2>
      <hr class="transparent">
      <b-row v-masonry transition-duration="0.3s" item-selector=".col">
        <b-col v-masonry-tile col lg="4" sm="6" :key="index" v-for="(work,index) in works">
          <img :src="`images/works/${work.imgSrc}`" alt="">
          <div class="overlay-layer">
            <span>
              <a v-bind:href="work.linkUrl" target="_blank">
                <i class="fas fa-link"></i>
                {{ work.title }}
              </a>
            </span>
          </div>
        </b-col>
      </b-row>
    </b-container>
  </div>
</template>

<script>
import {VueMasonryPlugin} from 'vue-masonry'

export default {
  name: 'work',
  created() {
    this.$http.get('/api/works')
    .then((response) => {
      this.works = response.data
      console.log('데이터 로드 성공')
      //console.log(response)
    }).catch((error) => {
      console.log('데이터 로드 실패')
      console.log(error)
    });
  },
  data() {
    return {
      works: []
    }
  },
}
</script>

<style scoped>
  .work-bg {
    padding: 40px 0;
  }
  .row {
    margin: 0 -7px;
  }
  .col {
    position: relative;
    padding: 7px;
  }

  img {
    max-width: 100%;
    border: 1px #dedede solid;
    display: block;
  }

  .overlay-layer {
    opacity: 0;
    position: absolute;
    top: 0;
    right: 0;
    left: 0;
    bottom: 0;
    background-color: rgba(0,0,0,0.5);
    margin: 7px;
    transition: all .2s ease-in-out;
  }

  .overlay-layer:hover {
    opacity: 1;
  }

  .overlay-layer span {
    position: absolute;
    text-align: center;
    left: 0;
    right: 0;
    top: 50%;  
  }

  .overlay-layer span a {
    border: 1px solid #fff;
    width: auto;
    display: inline-block;
    padding: 8px 20px;
    color: #fff;
    background: rgba(0,0,0,0.0);
    letter-spacing: 2px;
    word-spacing: 5px;
    margin-top: -42px;
    transition: all .30s ease-in-out;
    text-decoration: none;
  }

  .overlay-layer:hover span a {
    background: rgba(0,0,0,0.6);
  }
</style>
