<template>
  <div class="home">
    <mt-header fixed title="懒人点餐">
      <router-link to="/menu" slot="right">
        <mt-button>菜单设置</mt-button>
      </router-link>
    </mt-header>
    <div id="myBody">
      <h1>{{ msg }}</h1>
      <router-link to="/order" >
        <mt-button type="primary">随机点餐</mt-button>
      </router-link>
      <p>{{ btnHint }}</p>
    </div>
  </div>
</template>

<script>
export default {
  name: 'home',
  data () {
    return {
      msg: '欢迎体验懒人点餐!',
      btnHint: '请点击进行随机选择'
    }
  },
  created: function () {
    if (window.localStorage.getItem('menuList') === null) {
      window.localStorage.setItem('menuList', '["炒面","炒年糕","炒饭"]')
    }
  }
}
</script>
<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.home {
  position: fixed;
  text-align: center;
  background-color: aquamarine;
  height: 100%;
  width: 100%;
  margin: 0px;
}
#myBody {
  position: relative;
  top: 50%;
  transform: translateY(-50%);
}
</style>
