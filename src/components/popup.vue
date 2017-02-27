<template>
  <div class="popup">
    <div class="inserter-list" v-show="isInsert == true">
      <button @click="addText()">{{text}}</button>
      <button @click="addImg">{{img}}</button>
      <button @click="addBtn">{{btn}}</button>
    </div>
    <div class="inserter" v-show="isInsert == false" @click="toggleInsert">
      <button class="inserter-container inserter-add">+</button>
    </div>
  </div>

</template>
<script>
export default{
  data () {
    return {
      text: 'Insert Text',
      img: 'Insert Image',
      btn: 'Insert Button',
      isInsert: false
    }
  },
  props: {
    addComponents: Function
  },
  methods: {
    addText: function () {
      this.$emit('up', 'componentText')
      this.toggleInsert()
      this.addComponent()
    },
    addImg: function () {
      this.$emit('up', 'componentImg')
      this.toggleInsert()
      this.addComponent()
    },
    addBtn: function () {
      this.$emit('up', 'componentBtn')
      this.toggleInsert()
      this.addComponent()
    },
    toggleInsert: function () {
      this.isInsert = !this.isInsert
    },
    addComponent: function (data) {
      return this.addComponents()
    }
  }
}
</script>
<style scoped>
.popup{
  display: block;
  position: absolute;
  left: -95px;
  top:-2px;
  z-index: 100;
  width: 100%
}
/*.popup:after{
  left:32px;
  top:calc(50% - 0px);
  display: block;
  content: '';
  width: 100%;
  height: 50%;
  border-top: #eee 1px dashed;
}*/
  /*.inserter-list:before, .inserter:before{
    position: absolute;
    display: block;
    top: 50%;
    content: '\25B8';
    transform: translateY(-50%);
    right: -7px;
    text-shadow: 1px 2px 6px rgba(0,0,0,.1);
    color: rgba(0,0,0,.1);
  }
  .inserter-list:after, .inserter:after{
    color:#fff;top: 50%;
    content: '\25B8';
    transform: translateY(-50%);
    left:auto;
    position: absolute;
    display: block;
    right: -6px;}*/
  .inserter-add, .inserter-list{
    background: #fff;
    border: none;
    right: -6px;
    width:30%;
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
