<template>
  <div class="container">
    <search :getName="getName"></search>
    <demo-main :userName="userName"></demo-main>
  </div>
</template>


<script>
  import search from './search.vue'
  import main from './main.vue'
  export default {
      components: {
          search,
        'demo-main': main
      },
    data () {
          return {
              userName: ''
          }
    },
    methods: {
          getName (userName) {
              this.userName = userName
          }
    }
  }
</script>


<style></style>
