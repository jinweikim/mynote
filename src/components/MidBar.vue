<template>
  <div>
    <el-table
      :data="articleList"
      style="width: 100%"
      stripe
      :fit=false
      :show-header=false
      @cell-click="handleClick">
      <el-table-column
        label="标题"
        prop="title"
        width="300">
      </el-table-column>
    </el-table>
  </div>
</template>

<script>
export default {
  name: 'MidBar',
  props: {
    articleList: {
      type: Array,
      required: true
    }
  },
  methods: {
    handleClick (row, column, event, cell) {
      // console.log(key, keyPath)
      console.log(row.id)
      // 先传送给上层 LeftBar
      this.$emit('choose-article', row.id)
    }
  }
}
</script>

<style scoped>

</style>
