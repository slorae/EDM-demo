<template>
<!--  -->
  <li class="text">
    <input type="text" name="" placeholder="请输入内容">
    <div @mouseenter.stop="show($event)" @mouseleave.stop="showPopup = false" class="popupBox">
      <component-popup v-show="showPopup" class="popup" @up="choice" :addComponents="addComponents.bind(this, result)">
      </component-popup>
    </div>
  </li>
</template>
<script>
import componentPopup from './popup'
export default {
  data () {
    return {
      showPopup: false,
      result: ''
    }
  },
  props: {
    onHandleClick: Function
  },
  methods: {
    show: function (event) {
      this.showPopup = true
    },
    choice: function (msg) {
      this.result = msg
    },
    addComponents: function (data) {
      return this.onHandleClick()
    }
  },
  components: { componentPopup }
}
</script>
<style scoped>
  .text{width: 100%;border: 1px dotted #eee; padding: 10px 5px;margin-bottom: 10px;}
   .text input{border: none;outline: none;}
</style>
