<template>
  <div class="VueStar"> 
    <div class="VueStar__ground">
      <div class="VueStar__icon" @click="toggle" :class="AnimateClass" :style='{color:ColorValue}'>
        <slot name="icon"></slot>
      </div>
      <div class="VueStar__decoration" :class="{ 'VueStar__decoration--active':active}"></div>
    </div>
  </div>
</template>

<script>
import { isColors } from '../uitls/colorRE.js'
export default {
  name: 'VueStar',
  props: {
    animate: String,
    color: String,
    status: Boolean
  },
  methods: {
    toggle () {
      this.active = !this.active
      this.toggleAnimate = !this.toggleAnimate
      this.toggleColor = !this.toggleColor
    }
  },
  data () {
    return {
      active: this.status,
      toggleAnimate: this.status,
      toggleColor: this.status
    }
  },
  computed: {
    AnimateClass () {
      return this.toggleAnimate ? this.animate : ''
    },
    ColorValue () {
      return this.toggleColor ? this.color : ''
    }
  },
  mounted () {
    console.log(this.active, this.toggleAnimate, this.toggleColor)
    if (this.color) {
      if (isColors(this.color)) {
        return
      } else {
        console.error('this color must be hexcolor or rgbcolor  ---VueStar')
      }
    } else {
      return
    }
  }
}
</script>

<style lang="less">
 @import '../style/main.less';
</style>