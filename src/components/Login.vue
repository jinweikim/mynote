<template>
  <div class="login">
    <h1 v-text="title"></h1>
    <input type="text" v-model="newItem">
    <button @click="addNewItem"> 添加 </button>
    <li v-for="item in items" :key="item.id">
      <span v-text="item.title"> </span>
      <button @click="toggleFinish(item)">完成</button>
    </li>
  </div>
</template>

<script>
// import index from '../router'

export default {
  name: 'Login',
  data () {
    return {
      title: '请登录',
      id: 0,
      newItem: '',
      items: []
    }
  },
  methods: {
    toggleFinish (recycleItem) {
      this.items.map((item, index) => {
        if (item.id === recycleItem.id) {
          this.items.splice(index, 1)
        }
      })
    },

    addNewItem () {
      this.items.push({
        id: this.id,
        title: this.newItem
      })

      this.id++
      this.newItem = ''
    }
  }
}
</script>

<style scoped>

</style>
