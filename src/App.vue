<template>
  <div class="container-fluid">
    <div class="row p-3 gap-3">
      <Question1 msg="Welcome to Your Vue.js App"/>
      <Question2 msg="Welcome to Your Vue.js App"/>
      <Question3 msg="Welcome to Your Vue.js App"/>
    </div>
  </div>
</template>

<script>
import Question1 from './components/Question1.vue'
import Question2 from './components/Question2.vue'
import Question3 from './components/Question3.vue'

export default {
  name: 'App',
  components: {
    Question1, Question2, Question3
  }
}
</script>

<style>
</style>
