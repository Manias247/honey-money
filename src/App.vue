<template>
  <Navbar v-bind:members="loginMembers"
  :name="name"
  :backgroundPic="backgroundPic"
  @edit-thumbnail="editThumbnail"
  :activePersonId="activeId"/>
  
  <Welcome
  v-if="!statusLogin"
  :name="name"
  :backgroundPic="backgroundPic"
  :activePersonId="activeId"
  v-bind="members"
  @back-login="backLogin"
    @show-login="showLoginBox"
    :status-admin="statusAdmin"
    
    @login-homer="loginHomer" 
    @login-merge="loginMerge" 
    @login-lisa="loginLisa" 
    @login-bart="loginBart" 
    @login-maggie="loginMaggie" 
  />
  <Homer
  v-if="statusHomer"/>
  <Merge
  v-if="statusMerge"/>
  <Lisa
  v-if="statusLisa"/>
  <Bart
  v-if="statusBart"/>
  <Maggie
  v-if="statusMaggie"/>
</template>

<script>
import Navbar from "./components/Navbar.vue";
import Welcome from "./components/Welcome.vue";
import Homer from "./components/Homer.vue";
import Merge from "./components/Merge.vue";
import Lisa from "./components/Lisa.vue";
import Bart from "./components/Bart.vue";
import Maggie from "./components/Maggie.vue";
export default {
  name: "App",
  props: ["members", "activePersonId", "backgroundPic", "name" ],

  components: {
    Navbar,
    Welcome,
    Homer,
    Merge,
    Lisa,
    Bart, 
    Maggie
  },
  data() {
    return {
      loginShow: false,
      statusAdmin: false,
      statusLogin: false,
      statusHomer: false,
      statusMerge: false,
      statusLisa: false,
      statusBart: false,
      statusMaggie: false,
    };
  },
  methods: {
    loginHomer(active){
      this.statusHomer = true;
      this.activeId = active
      console.log(active)
      this.statusLogin = true;
    },
    loginMerge(){
      this.statusMerge = true;
      
      this.statusLogin = true;
    },
    loginLisa(){
      this.statusLisa = true;
      this.statusLogin = true;
    },
    loginBart(){
      this.statusBart = true;
      this.statusLogin = true;
    },
    loginMaggie(){
      this.statusMaggie = true;
      this.statusLogin = true;
    },

  }
}


      

      

</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: Inter, system-ui, Avenir, Helvetica, Arial, sans-serif;
}
body {
  background-color: rgba(170, 225, 255, 0.667);
}


</style>
