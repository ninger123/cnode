<template>
  <div id="app">
    <Header></Header>
    <div class="main">
      <router-view name="main"></router-view>
    </div>
  </div>
</template>

<script>
  import Header from "./components/header"
  import PostList from "./components/PostList"
export default {
  name: 'App',
  components:{
    Header,
    PostList
  }
}
</script>

<style>
  *{
    margin: 0;
    padding: 0;
  }
  body{
    margin: 0;
    padding: 0;
  }
  .main{
    background-color: rgb(225,225,225);
  }

</style>
