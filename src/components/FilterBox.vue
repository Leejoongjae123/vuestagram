<template>
  <div :class="`filter-item ${filter}`" :style="`background-image:url(${imageUrl})`">
    <span style="color:red">{{filter}}</span>
  </div>

</template>

<script>
export default {
  name:'filterbox',
  props:{
    imageUrl:String,
    filter:String
  }
}
</script>

<style>
.filter-item {
  width: 100px;
  height: 100px;
  margin: 10px 10px 10px auto;
  padding: 8px;
  display: inline-block;
  color : white;
  background-size: cover;
  background-position : center;
}
.filter-name{
  color:black;
}
</style>