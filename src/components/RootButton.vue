<template lang="html">
  <div>
    <div v-if='debugHint' id="debug">{{hintText}}</div>
    <b-img :src='icon' id='rootButton' @contextmenu.prevent @touchstart="touchstart($event)"
      @touchmove="touchmove($event)"
      @touchend="touchend($event)"/>
    <div id="mask" v-show="maskShow" class="container-fluid">
      <div class='content row'></div>
      <div class='sub-buttons row'>
        <SubButton v-for='btn in btns'
          :key='btn.value'
          :name='btn.name'
          :value='btn.value'
          :icon='btn.icon'
          :active-icon='btn.activeIcon'
          :active='activeBtnValue==btn.value'/>
      </div>
    </div>
  </div>
</template>

<script>
import $ from 'jquery';
import _ from 'lodash/core';
import SubButton from './SubButton.vue';

export default {
  data: function(){
    return {
      state:'none',
      hitButton:null,
      activeBtnValue:'index',
    };
  },
  props:{
    btns:{
      type:Array,
    },
    icon:'',
    debugHint:{
      type:Boolean,
      default:false,
    },
  },
  components:{
    SubButton:SubButton,
  },
  methods:{
    touchstart:function(e){
      this.state = "start";
    },
    touchmove:function(e){
      var touchX = e.changedTouches[0].clientX;
      var touchY = e.changedTouches[0].clientY;
      this.hitButton = this.getHitButton(touchX, touchY, $(".sub-button"));
      this.activeBtnValue = $(this.hitButton).attr('data-value');

      //reset
      this.resetButtonsStyles();

      $(this.hitButton).find('img').width('64px').height('64px');
      $(this.hitButton).find('p').css('color','#7f2828');

      this.state = "move";
    },
    touchend:function(e){
      var touchX = e.changedTouches[0].clientX;
      var touchY = e.changedTouches[0].clientY;
      this.hitButton = this.getHitButton(touchX, touchY, $(".sub-button"));

      //reset
      this.resetButtonsStyles();

      this.state = "end";
    },
    hitDetect:function(touchX,touchY,rect){
      return ((touchY>rect.top) && (touchY<rect.bottom)) && ((touchX>rect.left) && (touchX < rect.right))
    },
    getHitButton:function(touchX, touchY, $buttons){
      var target = null;
      var _this = this;
      if($buttons.length > 0){
        $buttons.each(function(i, button){
          if(_this.hitDetect(touchX,touchY,button.getBoundingClientRect())){
            target = button;
          }
        });
      }
      return target;
    },
    resetButtonsStyles:function(){
      $(".sub-button").each(function(i,button){
        $(button).find('img').width('48px').height('48px');
        $(button).find('p').css('color','#adadad');
      });
    },
    getActiveBtn: function(){
      return _.find(this.btns, {'value':this.activeBtnValue});
    },
  },
  computed:{
    maskShow:function(){
      return this.state=='start'||this.state=='move';
    },
    hintText:function(){
      switch(this.state){
        case "none":{
          return "按住按钮不放!";
        }
        case "start":{
          return "滑动手指!";
        }
        case "move":{
          return "继续滑动!";
        }
        case "end":{
          if(this.getActiveBtn())
            return "你选择的是'" + this.getActiveBtn().name + "'";
          else
            return "滑动被取消了，按住按钮不放!";
        }
      }
    },
  },
}
</script>

<style lang="css">
#rootButton{
  position:fixed;
  bottom:3em;
  width:4em;
  height:4em;
  left:0;
  right:0;
  margin:0 auto;
  text-align:center;
  z-index: 500;
  touch-action: none;
}

.sub-button{
  z-index:500;
  touch-action: none;
}

.sub-button p{
  margin:0;
  font-family: 'Vera Sans YuanTi Mono';
  font-size: 0.7em;
  font-weight: bold;
}

#mask{
  position:fixed;
  top:0;
  width:100%;
  height:100%;
  z-index: 50;
  background-color: rgba(255,255,255,0.2);
}

#mask .content{
  min-height:65%;
}
</style>
