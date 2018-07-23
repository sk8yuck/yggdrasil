<template lang="html">
  <div>
    <div id="debug">{{state}}</div>
    <div id='rootButton' @touchstart="touchstart($event)"
      @touchmove="touchmove($event)"
      @touchend="touchend($event)">
    </div>
    <div id="mask" v-show="maskShow">
      <div class='sub-button' ref='subButtons'
        v-for='no in [1,2,3]' :id="'sub-button-'+no" :data-value="no">{{no}}</div>
    </div>
  </div>
</template>

<script>
export default {
  data: function(){
    return {
      state:'none',
    };
  },
  methods:{
    touchstart:function(e){
      this.state = "start";
    },
    touchmove:function(e){
      var touchX = e.changedTouches[0].clientX;
      var touchY = e.changedTouches[0].clientY;
      var hitButton = this.getHitButton(touchX, touchY, this.$refs.subButtons);

      if(hitButton){
        hitButton.setAttribute('style', "width:4em;height:4em;");
      }else{
        this.$refs.subButtons.forEach(function(button){
          button.setAttribute('style', "width:3em;height:3em;");
        });
      }

      this.state = "move";
    },
    touchend:function(e){
      var touchX = e.changedTouches[0].clientX;
      var touchY = e.changedTouches[0].clientY;
      var hitButton = this.getHitButton(touchX, touchY, this.$refs.subButtons);

      this.state = hitButton?hitButton.getAttribute("data-value"):"none";
    },
    hitDetect:function(touchX,touchY,rect){
      return ((touchY>rect.top) && (touchY<rect.bottom)) && ((touchX>rect.left) && (touchX < rect.right))
    },
    getHitButton:function(touchX, touchY, buttons){
      var target = null;
      var _this = this;
      buttons.map(function(button, i){
        if(_this.hitDetect(touchX,touchY,button.getBoundingClientRect())){
          target = button;
        }
      });
      return target;
    },
  },
  computed:{
    maskShow:function(){
      return this.state=='start'||this.state=='move';
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
  border-radius: 100%;
  background-color: green;
}

.sub-button{
  float:left;
  margin:0.5em;
  width:3em;
  height:3em;
  z-index:500;
  border-radius: 100%;
  background-color: green;
}

#mask{
  position:fixed;
  top:0;
  width:100%;
  height:100%;
  z-index: 50;
  background-color: rgba(0,0,0,0.5);
}
</style>
