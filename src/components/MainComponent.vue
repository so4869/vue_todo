<template>
  <div class="jumbotron">
    <h1 class="display-4">Hello Vue.js Todo App</h1>
    <p class="lead">어서요세요. 또제수업에</p>
    <hr class="my-4">
    <p>웰컴이고 나발이고 집에가서 쉬고싶다.</p>
    <p class="lead">
      <router-link to="/todo" class="btn btn-primary">일정보기</router-link>
    </p>
  </div>
</template>

<script>
export default {
    name: 'main-compo',
    data () {
        return {}
    }
}
</script>

<style>
</style>
