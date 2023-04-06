<template>
  <header>
 
    <h1 class="title">honey where's your money</h1>
    <div class="user">
      <h3 class="user-name"></h3>
      <img id="user-photo-container"/>
      
      <div class="options-dots">...</div>
    </div>
  </header>
</template>

<script>
// import imageHomer from "./images/images/homer.jpg";
// import imageMerge from "./images/images/merge.png";
// import imageLisa from "./images/images/lisa.png";
// import imageMaggie from ".//images/images/maggie.png";
// import imageBart from "./images/images/bart.png";
export default {
  name: "Navbar",
  data() {
    return {
    
    };
  },
  props: ["members", "name", "backgroundPic"],
  methods: {
    editThumbnail(){
      let photoContainer = document.getElementById("user-photo-container")
      photoContainer.src = backgroundPic
    }
    // setUserImage(activePersonImage){
    //   
    // }
  },
};
</script>

<style scoped>
nav {
  width: 100%;
  height: 60px;
  display: flex;
  justify-content: center;
  align-items: center;
}

header {
  width: 100%;
  
  background-color: rgb(46, 73, 161);
  color: aliceblue;
  /* color: #FFD90F; */
  display: inline-flex;
  justify-content: space-evenly;
  align-items: center;
  min-height: 12vh;
}
.title {
  margin: 0;
}
</style>
