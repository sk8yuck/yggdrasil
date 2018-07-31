<template>
  <div id="app">
    <b-img src="./assets/logo.png"/>
    <RootButton :btns="btnData.btns" :icon="btnData.icon" :debug-hint='true'/>
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
  data:function(){
    return {
      btnData:{
        icon:require('./assets/root_btn.png'),
        btns:[
          {
            name:"首页",
            icon:require("./assets/index_icon.png"),
            activeIcon:require("./assets/index_icon_active.png"),
            value:"index"
          },
          {
            name:"乐馆",
            icon:require("./assets/gallery_icon.png"),
            activeIcon:require("./assets/gallery_icon_active.png"),
            value:"gallery"
          },
          {
            name:"乐迷广场",
            icon:require("./assets/plaza_icon.png"),
            activeIcon:require("./assets/plaza_icon_active.png"),
            value:"plaza"
          },
          {
            name:"个人中心",
            icon:require("./assets/member_icon.png"),
            activeIcon:require("./assets/member_icon_active.png"),
            value:"member"
          },
        ],
      },
    };
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
