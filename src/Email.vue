<template>
  <div id="email">
    <div class="top">
      <input type="text" placeholder="Enter your email subject">
      <div class="sender_date">
        <p class="sender">
          xxx from xxx
        </p>
        <p class="date">xx xx,xxxx</p>
      </div>
    </div>
    <div class="body" >
      <!-- <div @mouseenter.stop="showPopup = true" @mouseleave.stop="showPopup = false" class="popupBox">
        <component-popup v-show="showPopup" class="popup" @up="choice" @click="choice" :addComponents="add.bind(this, result)"  >
        </component-popup>
      </div>
      <ul>
        <li :is="item.component" v-for="item in items">
          <component :is="currentComponent" message="hahaha" :onHandleClick="add.bind(this, 'componentBtn')" ></component>
        </li>
         <component :is="item.component" v-for="item in items" :onHandleClick="add.bind(this, result)" @up="choice" ></component>
      </ul>
    </div> -->
      <div class="inserter-content">
        <component-inserter @choiceType='showType' :onHandleClick="add.bind(this, index, type)" :index="index" v-for="(item, index) in items"></component-inserter>
      </div>
    </div>
</template>

<script>
import componentInserter from './components/inserter'
export default {
  data () {
    return {
      items: [{
        component: componentInserter,
        type: ''
      }]
    }
  },
  methods: {
    add: function (idx, type) {
      this.items.push({
        'component': componentInserter,
        'type': this.type
      })
      // console.log(idx)
      // console.log(type)
    },
    showType: function (msg) {
      this.type = msg
      console.log(this.type)
    }
  },
  components: { componentInserter },
  name: 'email'
}
</script>

<style>
#email{width: 50%;margin: 0 auto;border: 1px solid #eee;padding: 10px;}
  .top input{width: 90%;padding-left: 5px;}
  .sender_date{display: flex;}
    .sender{flex: 1;color:#666; }
    .date{flex: 0 0 auto;color: #999;}
  .body{padding: 35px;border: 1px solid #ddd;position: relative;}
  .popupBox{height: 20px;background: #f00;position: relative;}
    .popup{position: absolute;}
  ul{width: 100%;padding: 0;}
  li{list-style: none;}
</style>
