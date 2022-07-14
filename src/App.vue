<template>
  <div class="header">
    <ul class="header-button-left">
      <li>Cancel</li>
    </ul>
    <ul class="header-button-right">
      <li v-if="step<=1" @click="step++">Next</li>
      <li v-if="step==2" @click="publish">Post</li>
    </ul>
    <img src="./assets/logo.png" class="logo" />
  </div>
  <Container @write="write" :data="data" :step="step" :imageUrl="imageUrl"/>

  <div class="footer">
    <ul class="footer-button-plus">
      <input @change="upload" type="file" id="file" class="inputfile" />
      <label for="file" class="input-plus">+</label>
    </ul>
  </div>  

</template>

<script>
import Container from './components/Container';
import data from './assets/data'
import axios from 'axios'


export default {
  data(){
    return{
      data:data,
      noClick:0,
      step:0,
      imageUrl:"",
      message:""
    }
  },
  name: 'App',
  components: {
    Container:Container
  },
  methods:{
    more(){
      console.log(this.noClick);
      if(this.noClick>=1){
        axios.get('https://codingapple1.github.io/vue/more1.json')
        .then((result)=>{
          console.log(result.data)
          this.data.push(result.data)
        })        
      } else{
        axios.get('https://codingapple1.github.io/vue/more0.json')
        .then((result)=>{
          console.log(result.data)
          this.data.push(result.data)
        })                
      }
      this.noClick++;
    },
    upload(e){
      let 파일 = e.target.files
      // console.log(파일[0])
      this.imageUrl=URL.createObjectURL(파일[0])
      this.step=1;
      
    },
    publish(){
      var myPosting={
        name: "Kim Hyun",
        userImage: "https://placeimg.com/100/100/arch",
        postImage: `${this.imageUrl}`,
        likes: 36,
        date: "May 15",
        liked: false,
        content: this.message,
        filter: "perpetua"        
      };
      this.data.unshift(myPosting)
      this.step=0;
      console.log("message:",this.message)
    },
    write(event){
      this.message=event
    }
  }

}
</script>

<style>
body {
  margin: 0;
}
ul {
  padding: 5px;
  list-style-type: none;
}
.logo {
  width: 22px;
  margin: auto;
  display: block;
  position: absolute;
  left: 0;
  right: 0;
  top: 13px;
}
.header {
  width: 100%;
  height: 40px;
  background-color: white;
  padding-bottom: 8px;
  position: sticky;
  top: 0;
}
.header-button-left {
  color: skyblue;
  float: left;
  width: 50px;
  padding-left: 20px;
  cursor: pointer;
  margin-top: 10px;
}
.header-button-right {
  color: skyblue;
  float: right;
  width: 50px;
  cursor: pointer;
  margin-top: 10px;
}
.footer {
  width: 100%;
  position: sticky;
  bottom: 0;
  padding-bottom: 10px;
  background-color: white;
}
.footer-button-plus {
  width: 80px;
  margin: auto;
  text-align: center;
  cursor: pointer;
  font-size: 24px;
  padding-top: 12px;
}
.sample-box {
  width: 100%;
  height: 600px;
  background-color: bisque;
  text-align: center;
}
.inputfile {
  display: none;
}
.input-plus {
  cursor: pointer;
}
</style>
