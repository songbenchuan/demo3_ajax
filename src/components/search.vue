<template>
  <div>
    <section class="jumbotron">
      <h3 class="jumbotron-heading">Search Github Users</h3>
      <div>
        <input type="text" placeholder="enter the name you search" v-model="userName"/>
        <button @click="search">Search</button>
      </div>
    </section>
  </div>
</template>


<script>
  export default {
    props: ['getName'],
    data () {
        return {
            userName: ''
        }
    },
    methods: {
        search () {
            //判断用户输入的是否为空串
          if(!this.userName.trim()){
              return
          }
            this.getName(this.userName)
        }
    }
  }


</script>


<style></style>
