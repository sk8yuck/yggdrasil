<template>
  <div id="app">
    <img src="./assets/logo.png">
    <RootButton/>
  </div>
</template>

<script>
import RootButton from './components/RootButton';

export default {
  name: 'App',
  components: {
    RootButton,
  },
};
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

body{
  margin:0;
}
</style>
