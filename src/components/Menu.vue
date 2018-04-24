<template>
  <div class="menu">
    <mt-header fixed title="菜单">
      <router-link to="/" slot="left">
        <mt-button icon="back">返回</mt-button>
      </router-link>
    </mt-header>
    <div id="menuBody">
      <ul
        v-infinite-scroll="loadMore"
        infinite-scroll-disabled="loading"
        infinite-scroll-distance="10">
        <li v-for="item in list " :key="item.num">{{ item }}</li>
      </ul>
      <mt-button  @click="clearOrder" type="danger">清空菜单</mt-button>
      <mt-button  @click="addNewOrder" type="primary">添加新菜</mt-button>
    </div>
  </div>
</template>

<script>
import { MessageBox } from 'mint-ui'

export default {
  name: 'home',
  data () {
    return {
      msg: 'Welcome to 懒人点餐!',
      list: JSON.parse(window.localStorage.getItem('menuList'))
    }
  },
  methods: {
    addNewOrder: function () {
      MessageBox.prompt('请输入菜名').then(({ value, action }) => {
        this.list.push(value)
        window.localStorage.setItem('menuList', JSON.stringify(this.list))
      })
    },
    clearOrder: function () {
      MessageBox.confirm('是否要清空菜单?').then(action => {
        window.localStorage.removeItem('menuList')
        this.list = []
      })
    }
  }
}
</script>
<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.menu {
  position: fixed;
  text-align: center;
  background-color: aquamarine;
  height: 100%;
  width: 100%;
  margin: 0px;
}
ul {
  list-style-type: none;
}
#menuBody {
  position: relative;
  top: 50%;
  transform: translateY(-50%);
  }
</style>
