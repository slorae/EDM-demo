<template>
  <div class="image">
    <button @click="addImg">选择图片</button>
    <input type="file" name="" style="display: none" @change="addFile"/>
    <div @mouseenter.stop="show($event)" @mouseleave.stop="showPopup = false" class="popupBox">
      <component-popup v-show="showPopup" class="popup" @up="choice" :addComponents="addComponents.bind(this, result)">
      </component-popup>
    </div>
  </div>
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
    addImg: function () {
      this.$el.children[1].click()
    },
    addFile: function (item) {
      let img = document.createElement('img')
      let parent = document.getElementsByClassName('image')[0]
      parent.appendChild(img)
      img.setAttribute('src', this.$el.children[1].value)
      console.log(this)
    },
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
  .image{width: 100%;border: 1px dotted #eee; padding: 10px 5px;margin-bottom: 10px;}
    .image img{display: block;}
</style>
