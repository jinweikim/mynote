<template>
  <el-container style="height: 1000px;">
    <el-header>

    </el-header>
    <el-aside class="first_bar" width="600px">
      <LeftBar v-bind:folderGroupList="FolderGroupList" v-bind:articleList="currentArticleList" @choose-folder='receiveChooseFolder' @choose-article="receiveArticle" ref="left"></LeftBar>
    </el-aside>
    <el-main class="main">
<!--      <el-aside class="second_bar">-->
<!--        <MidBar v-bind:articleList="currentArticleList" ref="mid"> </MidBar>-->
<!--      </el-aside>-->
      <span> {{mainContent}}</span>
    </el-main>
  </el-container>
</template>

<script>
import LeftBar from './LeftBar'
import MidBar from './MidBar'
export default {
  name: 'Home',
  components: {LeftBar, MidBar},
  data () {
    return {
      FolderGroupList: [
        {id: 1, type: 'Search', name: 'Search', isActive: false, notebooks: [{id: 1, name: 'notebook1'}, {id: 2, name: 'notebook2'}]},
        {id: 2, type: 'Inbox', name: 'Inbox', isActive: false, notebooks: [{id: 1, name: 'notebook3'}, {id: 2, name: 'notebook4'}]},
        {id: 3, type: 'Favorites', name: 'Favorites', isActive: false, notebooks: [{id: 1, name: 'notebook5'}, {id: 2, name: 'notebook6'}]},
        {id: 4, type: 'CommonFolder', name: '学习', isActive: false, notebooks: [{id: 1, name: 'notebook7'}, {id: 2, name: 'notebook8'}]},
        {id: 5, type: 'CommonFolder', name: '工作', isActive: false, notebooks: [{id: 1, name: 'notebook9'}, {id: 2, name: 'notebook10'}]},
        {id: 6, type: 'Delete', name: 'Delete', isActive: false, notebooks: [{id: 1, name: 'notebook11'}, {id: 2, name: 'notebook12'}]}
      ],
      articleList: [
        {id: 1, notebooksName: 'notebook1', time: '2021/01/27', title: '测试文章1', content: '这是一篇测试文章1，写于 2021.1.27 14:56'},
        {id: 2, notebooksName: 'notebook1', time: '2021/01/27', title: '测试文章2', content: '这是一篇测试文章2，写于 2021.1.27 14:56'},
        {id: 3, notebooksName: 'notebook3', time: '2021/01/27', title: '测试文章3', content: '这是一篇测试文章3，写于 2021.1.27 14:56'},
        {id: 4, notebooksName: 'notebook5', time: '2021/01/27', title: '测试文章4', content: '这是一篇测试文章4，写于 2021.1.27 14:56'},
        {id: 5, notebooksName: 'notebook5', time: '2021/01/27', title: '测试文章5', content: '这是一篇测试文章5，写于 2021.1.27 14:56'},
        {id: 6, notebooksName: 'notebook7', time: '2021/01/27', title: '测试文章6', content: '这是一篇测试文章6，写于 2021.1.27 14:56'},
        {id: 7, notebooksName: 'notebook7', time: '2021/01/27', title: '测试文章7', content: '这是一篇测试文章7，写于 2021.1.27 14:56'},
        {id: 8, notebooksName: 'notebook8', time: '2021/01/27', title: '测试文章8', content: '这是一篇测试文章8，写于 2021.1.27 14:56'},
        {id: 9, notebooksName: 'notebook5', time: '2021/01/27', title: '测试文章9', content: '这是一篇测试文章9，写于 2021.1.27 14:56'},
        {id: 10, notebooksName: 'notebook5', time: '2021/01/27', title: '测试文章10', content: '这是一篇测试文章10，写于 2021.1.27 14:56'},
        {id: 11, notebooksName: 'notebook1', time: '2021/01/27', title: '测试文章11', content: '这是一篇测试文章11，写于 2021.1.27 14:56'},
        {id: 12, notebooksName: 'notebook1', time: '2021/01/27', title: '测试文章12', content: '这是一篇测试文章12，写于 2021.1.27 14:56'},
        {id: 13, notebooksName: 'notebook3', time: '2021/01/27', title: '测试文章13', content: '这是一篇测试文章13，写于 2021.1.27 14:56'},
        {id: 14, notebooksName: 'notebook4', time: '2021/01/27', title: '测试文章14', content: '这是一篇测试文章14，写于 2021.1.27 14:56'},
        {id: 15, notebooksName: 'notebook2', time: '2021/01/27', title: '测试文章15', content: '这是一篇测试文章15，写于 2021.1.27 14:56'}
      ],
      currentNotebook: {id: 1, name: 'notebook1'},
      mainContent: 'Hi'
    }
  },
  computed: {
    // 更换中部的文章列表
    currentArticleList: function () {
      let currentArticleList = []
      for (let i = 0; i < this.articleList.length; i++) {
        if (this.articleList[i].notebooksName === this.currentNotebook.name) {
          currentArticleList.push(this.articleList[i])
        }
      }
      return currentArticleList
    }
  },
  methods: {
    // 接收左侧栏当前选中的笔记本，以此判断中部应该更换哪些文章
    receiveChooseFolder (chooseNotebook) {
      // console.log(chooseNotebook.name)
      this.currentNotebook = chooseNotebook
    },
    receiveArticle (id) {
      console.log('receive' + id)
      for (let i = 0; i < this.articleList.length; i++) {
        if (this.articleList[i].id === id) {
          this.mainContent = this.articleList[i].content
        }
      }
    }
  }
}
</script>

<style scoped>
  .main {
    padding: 0;
  }
  .aside {

  }
  .el-row  :last-child {
    margin-bottom: 0;
  }
  .el-col {
  }
  .bg-purple-dark {
    background: #99a9bf;
  }
  .first_bar{
    width: 200px;
    background: rgb(238, 241, 246);
  }
  .second_bar{
    background: #C2C2C2;
  }
  .third_bar{
    background: #F4F6F7;
  }
  .row-bg {
    background-color: #f9fafc;
  }

</style>
