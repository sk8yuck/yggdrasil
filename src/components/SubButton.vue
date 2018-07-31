<template lang="html">
  <div class='sub-button col' :data-value='value'>
    <b-img :src="btnImgPath"/>
    <p>{{name}}</p>
  </div>
</template>

<script>
export default {
  props:{
    name:String,
    value:String,
    icon:'',
    activeIcon:'',
    active:{
      default:false,
      type:Boolean,
    },
  },
  computed:{
    btnImgPath:function(){
      return this.active?this.activeIcon:this.icon;
    },
  },
};
</script>

<style lang="css">
</style>
