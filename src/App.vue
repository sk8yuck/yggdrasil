<template>
  <div id="app">
    <b-img src="./assets/logo.png"/>
    <RootButton/>
  </div>
</template>

<script>
import $ from 'jquery';
import RootButton from './components/RootButton';

$('body').on('touchmove',function(e){
  e.preventDefault();
});

export default {
  name: 'App',
  components: {
    RootButton,
  },
};
</script>

<style>
#app {
  @font-face {
    font-family: "Vera Sans YuanTi Mono";
    src:url("./assets/VeraSansYuanTiMono-Regular.ttf") format('truetype');
  }
  font-family: 'Vera Sans YuanTi Mono';
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #adadad;
  margin-top: 60px;
}

body{
  margin:0;
  background-color: #2c2c2c;
}

*{
  touch-action:none;
}
</style>
