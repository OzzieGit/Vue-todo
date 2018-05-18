<template>
  <div class="tabs">
  	<div class="length">{{ list.length }} 条记录</div>
    <p>
      <span v-for="item in filters" @click="toggle(item)" :class="[ filter == item.en ? 'active' : '' ]">{{ item.zn }} </span>
    </p>
    <b @click="delAll">{{ text }}</b>
  </div>
</template>

<script>
  export default {
    data(){
      return {
        filters:[{ en:'all', zn:'全部' }, { en:'complete', zn:'已完成' }, { en:'imperfectly', zn:'未完成' }],
        text:'清除全部'
      }
    },
    props:{
     list:{
      type:Array,
      required:true
    },
    filter:{
      type:String,
      required:true
    }
  },
  methods:{
    toggle(item){
      this.$emit('toggleTodo',item.en)
    },
    delAll(){
      this.$emit('delList');
    }
  },
  updated(){
    if(this.filter == "all"){
      this.text = '清除全部'
    }else if(this.filter == "complete"){
      this.text = '清除已完成'
    }else if(this.filter == "imperfectly"){
      this.text = '清除未完成'
    }
  }
}
</script>

<style>
.tabs{ height: 30px; line-height: 30px; overflow: hidden; padding: 15px 20px; background-color: rgba(255,255,255,0.7); border-radius: 10px; margin-top: 20px; color: #666; letter-spacing: 1px;}
.tabs .length{ float: left; width: 90px; }
.tabs p{ float: left; width: 280px; text-align: center; font-size: 0; }
.tabs p span{ display: inline-block; font-size: 12px; padding: 0 15px; border: 1px solid #999; border-radius: 6px; margin: 0 5px; cursor: pointer; color: #999; }
.tabs p span.active{ border: 1px solid rgba(175,47,47,0.4); color: rgba(175,47,47,0.7); }
.tabs b{ float: right; width: 88px; text-align: center; cursor: pointer; border: 1px solid rgba(175,47,47,0.4); border-radius: 6px; font-weight: 100; font-size: 12px; color: rgba(175,47,47,0.7); }
</style>
