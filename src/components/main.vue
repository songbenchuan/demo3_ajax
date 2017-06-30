<template>
  <div class="row">
    <h2 v-show="firstView">Enter name to search</h2>
    <h2 v-show="loading">Loading......</h2>
    <h2 v-show="error">网络错误，稍后再试</h2>
    <div v-show="users" class="card" v-for="user in users">
      <a :href="user.html_url" target="_blank">
        <img :src="user.avatar_url" style='width: 100px'/>
      </a>
      <p class="card-text">{{user.login}}</p>
    </div>
  </div>
</template>

<script>
  import axios from 'axios'
  export default {
      props: ['userName'],
      data () {
          return {
            firstView: true,
            loading: false,
            users: null,
            error: null
          }
      },
      watch: {
          userName: {
              handler (value) {
                  //更新发送请求的状态
                  this.firstView = false
                  this.loading = true
                  this.users = null
                  this.error = null
                  const url = `https://api.github.com/search/users?q=${this.userName}`
                  axios.get(url)
                    .then(response => {
                      //更新成功的状态
                      this.loading = false

                      this.users = response.data.items.map(item => {
                          return {
                            html_url: item.html_url,
                            avatar_url: item.avatar_url,
                            login: item.login
                          }
                      })
                    })
                    .catch(error => {
                        //更新失败的状态
                      this.loading = false
                      this.error = true
                        console.log('请求错误')
                    })

              }
          }
      }
  }
</script>


<style>
  .card {
    float: left;
    width: 33.333%;
    padding: .75rem;
    margin-bottom: 2rem;
    border: 1px solid #efefef;
    text-align: center;
  }

  .card > img {
    margin-bottom: .75rem;
    border-radius: 100px;
  }

  .card-text {
    font-size: 85%;
  }
</style>
