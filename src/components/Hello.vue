<template>
  <mu-paper class="bottom_nav">
    <mu-bottom-nav :value="bottomNav" shift @change="handleChange">
      <mu-bottom-nav-item to="/" value="首页" title="首页" icon="home"/>
      <mu-bottom-nav-item to="/publish" value="发布" title="发布" icon="subject"/>
      <mu-bottom-nav-item to="/message" value="消息" title="消息" icon="message"/>
      <mu-bottom-nav-item :to="person_path" value="个人" title="个人" icon="person"/>
    </mu-bottom-nav>
  </mu-paper>

</template>

<script>
export default {
  data () {
    return {
      bottomNav: '首页',
      person_path: '/person'
    }
  },
  created () {
    this.fatchData()
  },
  watch: {
    '$route': 'fatchData'
  },
  methods: {
    handleChange (val) {
      this.bottomNav = val
    },
    fatchData () {
      let accessToken = localStorage.getItem('accessToken')
      if (accessToken) {
        this.person_path = '/person'
      } else {
        console.log('打印')
        this.person_path = '/login'
      }
      if (this.$route.path === '/') {
        this.bottomNav = '首页'
      }
      if (this.$route.path === '/subject') {
        this.bottomNav = '发布'
      }
      if (this.$route.path === '/message') {
        this.bottomNav = '消息'
      }
      if (this.$route.path === '/login' || this.$route.path === '/person') {
        this.bottomNav = '人个'
      }
    }
  }
}
</script>
<style scoped>
.bottom_nav {
    height: 5rem;
    position: fixed;
    bottom: 0;
    left: 0;
    right: 0;
}
</style>
