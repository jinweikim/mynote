<template>
  <div>
    <el-container width="600px">
      <el-aside>
        <el-menu class="menu_title" @open="handleOpenMenu" @close="handleCloseMenu" refs="leftMenu">
          <el-submenu v-for="(folder,index) in folderGroupList" :index="''+index" :key="folder.id">
            <template slot="title"><i v-bind:class=menuImage(folder)></i> {{ folder.name }}</template>
            <el-menu-item-group>
<!--              <template slot="title">分组一</template>-->
              <el-menu-item :index="index+1+'-'+subIndex" v-for="(notebook,subIndex) in folder.notebooks" :key="notebook.id" @click.native="transFolderToHome(notebook)">{{ notebook.name }}</el-menu-item>
            </el-menu-item-group>
          </el-submenu>
        </el-menu>
      </el-aside>
      <el-main width="400px" class="mid">
<!--        <AbstractBlock v-for="(article, index) in articleList" :key="article.id" :article="article" :index="index" ref="abstract"></AbstractBlock>-->
        <MidBar v-bind:articleList="articleList" @choose-article="transArticleToHome"></MidBar>
      </el-main>
    </el-container>
  </div>
</template>

<script>
import AbstractBlock from './AbstractBlock'
import MidBar from './MidBar'
export default {
  name: 'leftBar',
  components: {MidBar, AbstractBlock},
  data () {
    return {
      openedImage: 'el-icon-folder-opened',
      closedImage: 'el-icon-folder',
      menuImageActive: {CommonFolder: 'el-icon-folder-opened', Inbox: 'el-icon-box', Favorites: 'el-icon-star-on', Search: 'el-icon-search', Delete: 'el-icon-delete-solid'},
      menuImageNotActive: {CommonFolder: 'el-icon-folder', Inbox: 'el-icon-box', Favorites: 'el-icon-star-off', Search: 'el-icon-search', Delete: 'el-icon-delete'}
    }
  },
  props: {
    folderGroupList: {
      type: Array,
      required: true
    },
    articleList: {
      type: Array,
      required: true
    }
  },
  computed: {
    menuImage () {
      return function (folder) {
        let imageType = folder.type
        // 点击目录时，更换文件夹的图标
        if (folder.isActive) {
          return this.menuImageActive[imageType]
        } else {
          return this.menuImageNotActive[imageType]
        }
      }
    }
  },
  methods: {
    handleOpenMenu (key, keyPath) {
      // console.log(key, keyPath)
      this.folderGroupList[key].isActive = true
    },
    handleCloseMenu (key, keyPath) {
      // console.log(key, keyPath)
      // console.log(this.$refs.leftMenu.activeIndex)
      this.folderGroupList[key].isActive = false
    },
    transFolderToHome (notebook) {
      console.log(notebook.name)
      this.$emit('choose-folder', notebook)
    },
    transArticleToHome (id) {
      console.log(id + 'in LeftBar')
      // 将子组件传送来的数据再传送给父组件
      this.$emit('choose-article', id)
    }
  }
}
</script>

<style scoped>
  .menu_title {
    text-align: left;
  }
  .mid {
    padding: 0;
  }
</style>
