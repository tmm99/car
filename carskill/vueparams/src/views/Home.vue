<!--
 * @Author: your name
 * @Date: 2019-11-06 16:21:40
 * @LastEditTime: 2019-11-30 11:23:29
 * @LastEditors: Please set LastEditors
 * @Description: In User Settings Edit
 * @FilePath: \vueparams\src\views\Home.vue
 -->
<template>
  <div class="home">
    <Page></Page>
  </div>
</template>

<script>
// @ is an alias to /src
import Page from '../components/Page.vue'
// import Floor from '../components/Floor.vue'

export default {
  name: 'home',
  components: {
   Page
  }
}
</script>
<style scoped lang="style.css">
    .home{
        width: 100%;
        height: 100%;
    }
</style>