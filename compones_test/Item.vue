<template>
  <li
    @mouseenter="handlerItem(true)"
    @mouseleave="handlerItem(false)"
    :class="myClass"
  >
    <label>
      <input type="checkbox" v-model="isCheck" />
      <span>{{ todo.content }}</span>
    </label>
    <button class="btn btn-danger" v-show="isShow" @click="deleteT">
      删除
    </button>
  </li>
</template>

<script type="text/ecmascript-6">
export default {
  props:{
    todo:Object,
    index:Number,
    deleteOne:Function,
    updateOne:Function
  },
  computed:{
    isCheck:{
      get(){
        return this.todo.isOver
      },
      set(val){
        this.updateOne(this.index,val)
      }
    }
  },
  data(){
    return{
      isShow:false,
      myClass:"leaveItem"
    }
  },
  methods: {
    handlerItem(flag){
      if(flag){
        this.myClass = 'enterItem'
      }else{
        this.myClass = 'leaveItem'
      }
      // flag?this.myClass = "enterItem":this.myClass = "leaveItem",
    this.isShow = !this.isShow
    },
    deleteT(){
      this.deleteOne(this.index)
    }
  },
}
</script>

<style scoped>
li {
  list-style: none;
  height: 36px;
  line-height: 36px;
  padding: 0 5px;
  border-bottom: 1px solid #ddd;
}

li label {
  float: left;
  cursor: pointer;
}

li label li input {
  vertical-align: middle;
  margin-right: 6px;
  position: relative;
  top: -1px;
}

li button {
  float: right;
  margin-top: 3px;
}

li:before {
  content: initial;
}

li:last-child {
  border-bottom: none;
}
.enterItem {
  background: #aaa;
}
.leaveItem {
  background: #fff;
}
</style>
