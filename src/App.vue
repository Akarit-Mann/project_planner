<template>
    <NavBar></NavBar>
  <router-view/>
</template>
<script>
import NavBar from './components/NavBar'
export default {
  components: { NavBar },
  
}
</script>
<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  max-width: 600px;
  margin: 50px auto;
  color: #2c3e50;
}

.main-nav{
    text-align: center;
    margin: 40px auto;
}
.main-nav a{
    display: inline-block;
    text-decoration: none;
    margin: 0 10px;
    color: #999;
    font-size: 18px;
}
a.router-link-active{
    border-bottom: 4px solid #00CE89
;
    padding-bottom: 4px;
}

</style>
