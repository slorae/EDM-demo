<template>
  <li class="inserter-block">
    <div class="inserter-container">
      <div class="text" v-show="insertType == 'text'">
        <textarea placeholder="请输入内容" ></textarea>
      </div>
      <div class="image" v-show="insertType == 'image'">
        <button @click="addImg">选择图片</button>
        <img src="" v-show="">
        <input type="file" name="" style="display: none" @change="addFile"/>
      </div>
      <div class="btn" v-show="insertType == 'btn'">
        <button>Insert buttton</button>
      </div>
    </div>

    <div @mouseenter.stop="changePopStateEnter" @mouseleave.stop="changePopStateLeave" class="popupBox">
      {{showPopupList}}
      <div class="popup" v-show="showPopupList">
        <div class="inserter-list" v-show="isInsert == true">
          <button @click="addPopup('text', index)">Insert Text</button>
          <button @click="addPopup('image', index)">Insert Image</button>
          <button @click="addPopup('btn', index)">Insert Button</button>
        </div>
        <div class="inserter" v-show="isInsert == false" @click="toggleInsert">
          <button class="inserter-container inserter-add">+</button>
        </div>
      </div>
    </div>
  </li>
</template>
<script>
export default {
  data () {
    return {
      showPopupList: true,
      isInsert: false,
      insertType: 'text',
      items: [{component: 'div'}]
    }
  },
  // render: function (h) {
  //   this.items = []
  //   for (let i = 0; i < this.$el.length; i++) {
  //     this.items.push({component: this.$el.children[i]})
  //   }
  //   console.log(this.items)
  //   return h('div', {}, this.items)
  // },
  methods: {
    changePopStateEnter: function () {
      console.log('pop')
      console.log(this.showPopupList)
      this.showPopupList = true
      console.log(this.showPopupList)
    },
    changePopStateLeave: function () {
      console.log('leave')
      this.showPopupList = false
    },
    toggleInsert: function () {
      this.isInsert = !this.isInsert
    },
    addPopup: function (type, idx) {
      console.log(idx)
      this.toggleInsert()
      this.insertType = type
      // this.items.push({component: this.$el.children})
      this.items.push({component: 'div'})
      console.log(this.$el.children)
    },
    addImg: function () {
      // console.log(this.$el)
    },
    addFile: function (item) {
      let img = document.createElement('img')
      let parent = document.getElementsByClassName('image')[0]
      parent.appendChild(img)
      img.setAttribute('src', this.$el.children[1].value)
      // console.log(this.$el)
    }
  }
}
</script>
<style scoped>
.inserter-block{
  border:1px solid #000;
  position: relative;
  margin-bottom: 20px;
}
.inserter-block:before {
  display: block;
  content: '';

  position: absolute;
  bottom: 0;
  left: -20px;

  width: 20px;
  height: 30px;
  background-color: bisque;

}
  .text{
    width: 100%;
    height: auto;
    border: 1px dotted #eee;
    padding: 10px 5px;
    margin-bottom: 10px;
  }
   .text textarea{
    border: none;
    outline: none;
    resize: none;
    overflow: hidden;
    width: 100%;
  }
   .popup{
    display: block;
    position: absolute;
    left: -95px;
    top:-2px;
    z-index: 100;
    width: 100%
  }
  .inserter-add, .inserter-list{
    background: #fff;
    border: none;
    right: -6px;
    width:20%;
    border: 1px solid #eee;
  }
    .inserter-list button{
      display: block;
      padding:10px 0;
      border: none;
      color:#666;
      background: #fff;
      margin: 0 auto;
    }
    .inserter-list button:hover{
      color:#333;
    }
    .inserter-list button+button{
      border-top:1px solid #eee;
    }
</style>
