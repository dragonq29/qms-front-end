<template>
  <div id="app">
    <h1 >Post List</h1>
    <div>
      <post-list></post-list>
    </div>
  </div>
</template>

<script>
import PostList from './components/PostList.vue'

export default {
  name: 'App',
  components: {
    PostList
  }
}
</script>

<style>
</style>
