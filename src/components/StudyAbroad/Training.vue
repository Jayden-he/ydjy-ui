<template>
  <div id="training">
    <div class="sa-training-div">
      <img class="sa-training-bg" :src="bgImgUrl">
      <div class="sa-training-content">
        <div class="sa-training-txt" v-html="viewData.content"></div>
      </div>
    </div>
  </div>
</template>

<script>
  export default {
    name: 'Training',
    created() {
      // 组件创建完后获取数据，此时 data 已经被 observed 了
      this.fetchData()
    },
    watch: {
      // 如果路由有变化，会再次执行该方法
      '$route': 'fetchData'
    },
    data() {
      return {
        bgImgUrl: require('../../assets/img/study-abroad/training-bg.png'),
        viewData: {content:''}
      }
    },
    methods: {
      fetchData() {
        // Get获取数据
        this.axios.get(process.env.API_URL + 'media?id=21').then(response => {
          if (response.data.code === 1000) {
            this.viewData = response.data.data
          }
        })
      }
    }
  }
</script>

<style>
  .sa-training-div {
    margin: 0 -15px;
    position: relative;
  }
  .sa-training-bg {
    width: 100%;
  }
  .sa-training-content {
    position: absolute;
    background-color: rgba(100, 69, 145, 0.8);
    bottom: 0;
    width: 100%;
    height: 40%;
  }
  .sa-training-txt {
    position: absolute;
    left: 0;
    right: 0;
    top: 25%;
    margin: auto;
    width: 85%;
    height: 45%;
    color: white;
    line-height: 24px;
  }
</style>
