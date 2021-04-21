<template>
  <div>
    <div class="main odd" :class="{'even': oddOrEven}" @click="isChoose = true">
      <span>{{ article.time }}</span>
      <div>
        <span>{{ article.title }}</span>
      </div>
    </div>
    <div style="border:1px solid #CCC"></div>
  </div>

</template>

<script>
export default {
  name: 'AbstractBlock',
  comments: {},
  props: {
    article: {
      type: Object,
      required: true
    },
    index: {
      required: true
    }
  },
  data () {
    return {
      isChoose: false
    }
  },
  computed: {
    oddOrEven: function () {
      return (this.index + 1) % 2 !== 1
    }
  }
}
</script>

<style scoped>
  .main{
    height: 50px;
    text-align: left;
    padding-left: 20px;
  }

  .odd{
    background: white;
  }
  .even{
    background: gainsboro;
  }

</style>
