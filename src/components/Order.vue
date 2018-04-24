<template>
  <div id="order">
    <mt-header fixed title="懒人点餐">
      <router-link to="/" slot="left">
        <mt-button icon="back">返回</mt-button>
      </router-link>
    </mt-header>
    <div id="orderBody">
      <h1 >
        <strong>{{ msg }}</strong>
      </h1>
    </div>
    <div id="btnBody">
      <router-link to="/" >
        <mt-button type="primary">确认选餐</mt-button>
      </router-link>
      <mt-button @click="randomOrder" type="danger">再次随机</mt-button>
    </div>
  </div>
</template>
<script>
import { Indicator } from 'mint-ui'
export default {
  name: 'home',
  data () {
    return {
      msg: '今天吃什么呢？',
      list: JSON.parse(window.localStorage.getItem('menuList'))
    }
  },
  mounted () {
    this.init()
  },
  methods: {
    init () {
      this.list = JSON.parse(window.localStorage.getItem('menuList'))
      this.randomOrder()
    },
    randomOrder: function () {
      let _this = this
      this.msg = '今天吃什么呢？'
      Indicator.open({
        text: '正在随机选择中...',
        spinnerType: 'fading-circle'
      })
      setTimeout(function () {
        _this.showOrder()
      }, 2000)
    },
    showOrder: function () {
      Indicator.close()
      var order = this.list[Math.floor(Math.random() * this.list.length)]
      this.msg = '今天吃：' + order
    }
  },
  beforeDestroy () {
    Indicator.close()
  }
}
</script>

<style scoped>
#order {
  position: fixed;
  text-align: center;
  background-color: aquamarine;
  height: 100%;
  width: 100%;
  margin: 0px;
}
#orderBody {
  position: relative;
  top: 10%;
  /*transform: translateY(-200%);*/
}
#btnBody {
  position: relative;
  top: 50%;
  /*transform: translateY(-100%);*/
}
</style>
