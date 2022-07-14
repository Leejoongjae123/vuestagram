<template>
  <div>
    <div v-if="step==0">
      <Post v-for="(item,index) in data" :item="item" />
    </div>
    <!-- <Post :data="data"/>
    <Post :data="data"/> -->
  <div v-if="step==1">
    <div class="upload-image" :style="`background-image:url(${imageUrl})`"></div>
    <div class="filters">
      <FilterBox v-for="filter in filterList" :imageUrl="imageUrl" :filter="filter">
      </FilterBox>

    </div>  
  </div>
  
  <div v-if="step==2">
    <div class="upload-image" :style="`background-image:url(${imageUrl})`"></div>
    <div class="write">
      <textarea class="write-box" @input="$emit('write',$event.target.value)">write!</textarea>
    </div>  
  </div>
  <div>{{sendMessage}}</div>
</div>  
</template>

<script>
import Post from './Post.vue'
import FilterBox from './FilterBox.vue'

export default {
  name:"Container",
  data(){
    return{
      sendMessage:"",
      filterList:
      [ "aden", "_1977", "brannan", "brooklyn", "clarendon", "earlybird", "gingham", "hudson", 
        "inkwell", "kelvin", "lark", "lofi", "maven", "mayfair", "moon", "nashville", "perpetua", 
        "reyes", "rise", "slumber", "stinson", "toaster", "valencia", "walden", "willow", "xpro2"],
    }
  },
  components:{
    Post,
    FilterBox,
  },
  props:{
    data:Array,
    step:Number,
    imageUrl:String,
  },
  methods:{
  }

}
</script>

<style>
.upload-image{
width: 100%;
height: 450px;
background: cornflowerblue;
background-size : cover;
}
.filters{
overflow-x:scroll;
white-space: nowrap;
}
.filter-1 {
width: 100px;
height: 100px;
background-color: cornflowerblue;
margin: 10px 10px 10px auto;
padding: 8px;
display: inline-block;
color : white;
background-size: cover;
}
.filters::-webkit-scrollbar {
height: 5px;
}
.filters::-webkit-scrollbar-track {
background: #f1f1f1; 
}
.filters::-webkit-scrollbar-thumb {
background: #888; 
border-radius: 5px;
}
.filters::-webkit-scrollbar-thumb:hover {
background: #555; 
}
.write-box {
border: none;
width: 90%;
height: 100px;
padding: 15px;
margin: auto;
display: block;
outline: none;
}
</style>