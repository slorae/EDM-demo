<template>
<!--  -->
  <li class="btn">
    <button>{{btn}}</button>
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
      btn: 'Insert Button',
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
      this.$emit('up', this.result)
      console.log(11)
    },
    addComponents: function (data) {
      return this.onHandleClick()
    }
  },
  components: { componentPopup }
}
</script>
<style scoped>
  .btn{
    width: 100%;
    margin-bottom: 10px;
 }
    .insertedBtn{
      width: 150px;
      height: 50px;
      color: #fff;
      background: #666;
      border: none;
      cursor: pointer;
      border-radius: 5px;
    }
  .popupBox{height: 20px;background: #f00;position: relative;}
    .popup{position: absolute;}
</style>
