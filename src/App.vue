<template>
  <img alt="Vue logo" src="./assets/logo.png">
  <HelloWorld msg="Welcome to Your Vue.js App"/>

  <a href="/">Home</a> |
  <a href="/projects">Projects</a> |
  <a href="/actions">Actions</a>
  <component :is="currentView" />
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'
import ActionCalendar from './components/ActionCalendar.vue'
import ProjectList from './components/ProjectList.vue'
import NotFound from './components/NotFound.vue'

const routes = {
  '/': HelloWorld,
  '/projects': ProjectList,
  '/actions': ActionCalendar
}

export default {
  name: 'App',
  components: {
    HelloWorld
  },
  data() {
    return {
      currentPath: window.location.hash
    }
  },
  computed: {
    currentView() {
      return routes[this.currentPath.slice(1) || '/'] || NotFound
    }
  },
  mounted() {
    window.addEventListener('click', (e) => {
      e.preventDefault();
      window.history.pushState("", "", e.target.href);
      this.currentPath = e.target.href
    })
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>