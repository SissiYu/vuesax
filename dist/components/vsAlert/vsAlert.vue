<template lang="html">
  <transition name="fade">
    <div
      v-if="vsActive"
      v-bind="$attrs"
      :class="{
        'con-icon':vsIcon,
      }"
      :style="{
        'background':vsColor?/[#()]/.test(vsColor)?`rgba(${vsColor.replace(/[rgb()]/g,'')},.1)`:`rgba(var(--${vsColor}),.1)`:'rgba(var(--primary),.1)',
        'color':vsColor?/[#()]/.test(vsColor)?vsColor:`rgba(var(--${vsColor}),1)`:'rgba(var(--primary),1)',
        'margin-top':vsMargin,
        'margin-bottom':vsMargin,
      }"
      class="con-vs-alert"
      v-on="$listeners">

      <i
        v-if="vsIcon"
        translate="no"
        class="material-icons icon-alert notranslate">{{ vsIcon }}</i>

      <div
        v-if="vsClosable"
        class="con-x"
        @click="$emit('update:vsActive',false)">
        <i
          translate="no"
          class="material-icons notranslate">close</i>
      </div>

      <h3
        v-if="vsTitle"
        :style="{'background':'$primary'}"
        class="titlex">{{ vsTitle }}</h3>
      <div class="vs-alert">
        <slot/>
      </div>
    </div>
  </transition>
</template>

<script>
export default {
  name:'VsAlert',
  props:{
    vsActive:{
      type:[Boolean,String],
      default:false,
    },
    vsTitle:{
      type:String,
      default:null,
    },
    vsClosable:{
      type:Boolean,
      default:false,
    },
    vsColor:{
      type:String,
      default:null,
    },
    vsMargin:{
      type:[String,Boolean],
      default:'10px',
    },
    vsIcon:{
      type:String,
      default:null,
    }
  },
}
</script>

<style lang="css" scoped>

.titlex {
  padding: 15px;
  padding-bottom: 0px;
  font-weight: lighter;
}
.con-icon {
  display: flex;
  align-items: center;
  justify-content: center;
}
.icon-alert {
  position: relative;
  padding: 10px;
  display: flex;
  align-items: center;
  justify-content: center;
  padding-right: 0px;
  padding-left: 20px;
}
.con-x {
  position: absolute;
  right: 0px;
  top: 0px;
  width: 30px;
  height: 30px;
  border-radius: 50%;
  background: inherit;
  display: flex;
  align-items: center;
  justify-content: center;
  color: inherit;
  cursor: pointer;
  z-index: 100;
  transition: all .3s ease;
}
.con-x:hover {
  background: inherit;
  background: rgba(0, 0, 0, 0.5);
  color: rgb(255, 255, 255);
}
.con-x i {
  font-size: 1.0625em;
  color: inherit;
}
.fade-enter-active, .fade-leave-active {
  transition: all .3s;
}
.fade-enter, .fade-leave-to /* .fade-leave-active below version 2.1.8 */ {
  /* opacity: 0; */
  max-height: 0 !important;
  margin-bottom: 0px !important;
  margin-top: 0px !important;
}
.con-vs-alert {
  width: 100%;
  background: rgba(var(--primary),.1);
  border-radius: 10px;
  opacity: 1;
  overflow: hidden;
  position: relative;
  /* margin-top: 10px;
  margin-bottom: 10px; */
}
.vs-alert {
  color: inherit;
  padding: 15px;
  font-size: 0.9375em;
  position: relative;
}
.vs-alert b {
  color: rgba(var(--primary),1) !important;
}
</style>
