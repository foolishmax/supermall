<template>
    <div id="detail">
        <nav-bar class="nav-bar">
            <div slot="left" class="back" @click="backClick">
                <img src="~assets/img/common/back.svg" alt="">
            </div>
            <div slot="center" class="title">
                <div
                    class="title-item"
                    v-for="(item,index) in titles"
                    :class="{active: index === currentIndex}"
                    @click="clickItem(index)"
                >{{item}}</div>
            </div>
        </nav-bar>
    </div>
</template>

<script>
  import NavBar from 'components/common/navbar/NavBar'
  export default {
    name: 'Detail',
    data() {
      return {
        titles: ['商品','参数','评论','推荐'],
        currentIndex: 0
      }
    },
    methods: {
      clickItem(index){
        this.currentIndex = index
      },
      backClick() {
        this.$router.go(-1)
      }
    },
    components: {
      NavBar
    }
  }
</script>

<style scoped>
    .nav-bar {
        position: relative;
        z-index: 9;
        background-color: #fff;
    }
    .title {
        display: flex;
    }
    .title-item {
        flex: 1;
    }
    .active {
        color: var(--color-high-text);
    }
    .back img {
        margin-top: 12px;
    }
</style>
