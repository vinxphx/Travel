<template>
  <div class="icons">
    <swiper :options="swiperOption">
      <!-- slides -->
      <swiper-slide v-for="(page,index) of pages" :key="index">
        <div class="icon" v-for="item of page" :key="item.id">
          <div class="icon-img">
            <img class="icon-img-content" :src="item.imgUrl" alt />
          </div>
          <p class="icon-desc">{{item.desc}}</p>
        </div>
      </swiper-slide>

      <!-- Optional controls -->
      <div class="swiper-pagination" slot="pagination"></div>
    </swiper>
  </div>
</template>

<script>
export default {
  name: "HomeIcons",
  data() {
    return {
      swiperOption: {
        pagination: ".swiper-pagination"
      }
    }
  },
  props: {
    iconsList: Array
  },
  computed: {
    pages() {
      const pages = [];
      this.iconsList.forEach((item, index) => {
        const page = Math.floor(index / 8);
        if (!pages[page]) {
          pages[page] = [];
        }
        pages[page].push(item);
      });
      return pages;
    }
  }
};
</script>

<style lang="stylus" scoped>
@import '~@/assets/styles/varibles.styl';
@import '~@/assets/styles/mixins.styl';

.icons >>> .swiper-container {
  width: 100%;
  height: 0;
  padding-bottom: 55%;
}

.icons >>> .swiper-pagination {
  bottom: 0rem ;
}

.icons >>> .swiper-pagination-bullet-active {
  background: #555;
}

.icon {
  position: relative;
  overflow: hidden;
  width: 25%;
  float: left;
  padding-bottom: 25%;
  background: #fff;
  height: 0;
  margin-top .2rem
  .icon-img {
    position: absolute;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0.44rem;
    box-sizing: border-box;
    padding: 0.1rem;

    .icon-img-content {
      height: 100%;
      display: block;
      margin: 0 auto;
    }
  }

  .icon-desc {
    position: absolute;
    bottom: 0;
    left: 0;
    right: 0;
    line-height: 0.44rem;
    height: 0.44rem;
    text-align: center;
    color: $darkTextColor;
    ellipsis();
  }
}
</style>
