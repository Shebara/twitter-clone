<template>
  <div id="app">
    <Header :key="key" />
    <router-view :key="$route.path" class="p-5 container mx-auto" />
  </div>
</template>

<script>
import Header from './components/MainHeader.vue'

export default {
  name: 'App',
  components: {
    Header
  },
  data () {
    return {
      key: 0
    }
  },
  created() {
    try {
      const vm = this
      this.$watch(
        () => this.$route.params,
        () => {
          this.$store.dispatch('confirmLogin')
        }
      )
      this.$watch(
        () => this.$store.getters.getUserId,
        (userId) => {
          if (userId === false) {
            this.$router.push('/login')
          }
          vm.key++
        }
      )

      this.$store.dispatch('confirmLogin')
    } catch (e) {
      console.error(e);
    }
  }
}
</script>

<style>
#app {
  padding-bottom: 120px;
}
#app h1 {
  font-size: 2.2rem;
  font-weight: 700;
  text-align: center;
  margin-bottom: 40px;
}
#app h2 {
  font-size: 2rem;
  font-weight: 600;
}
#app h3 {
  font-size: 1.8rem;
  font-weight: 600;
}
#app h4 {
  font-size: 1.6rem;
  font-weight: 600;
}
#app h5 {
  font-size: 1.4rem;
  font-weight: 600;
}
#app h6 {
  font-size: 1.2rem;
  font-weight: 600;
}
#app form input, #app form textarea {
  border: 1px solid #777777;
  margin-bottom: 10px;
  padding: 10px;
}
#app form button {
  border: 1px solid #333333;
  background-color: #DFDFDF;
  padding: 10px;
}
#app form button:hover {
  background-color: #EFEFEF;
}
#app a {
  text-decoration: underline;
}
#app .small-avatar {
  width: 50px;
  height: 50px;
  border-radius: 50%;
  overflow: hidden;
  object-fit: cover;
}
</style>
