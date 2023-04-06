<template>
  <div>
    <button v-if="activePersonId != null" class="button back" @click="backLogin" id="back-login">Login another user</button>
    <h1 :class="{ hiddenwelcome: hideWelcome }" class="welcome-heading">Hello, {{ welcomeHeading }} </h1>
   

    
    <ul class="family-container">
      <li
        :class="{ hidden: isHidden }"
        v-for="person in members"
        :key="person.id"
        class="person"
      >
        <div :id="person.id">
          <div class="members-box">
            <div class="name">{{ person.name }}</div>

            <img
              @click="showLoginBox(person.id)"
              :id="person.id"
              class="image hvr-float-shadow"
              :src="person.backgroundPic"
            />
         </div>
        </div>
      </li>
    </ul>
    <div class="form-box">
      
      <form v-if="activePersonId != null" id="personForm" @submit.prevent="login(members[activePersonId].password)">
        <div>
        <h1 v-bind:value="members[activePersonId].name"> Hello {{ members[activePersonId].name}}</h1>
        <img class="image" :src="members[activePersonId].backgroundPic" />
      </div>
        <div id="password-error" class="user-input"> </div>
        <div  id="help-button" class="user-input"  :class="{ hiddenButton: isHiddenButton}" @click="showHint(members[activePersonId].hint)"></div>
        
        <div v-bind:value="members[activePersonId].hint" v-if="showHint"  id="password-hint" class="user-input" :class="{ hiddenHint: isHiddenHint}">  {{ members[activePersonId].hint}}</div>
      
        <label for="user-password">Your password</label>
        <input
          id="user-password"
          class="user-input"
          type="password"
          name="password"
          v-model="password"
          placeholder="Password"

        />
        <!-- v-bind:value="members[activePersonId].password" -->
        <input type="submit" value="login!" class="button submit" />
      </form>
    </div>
  </div>
</template>
<script>
import imageHomer from "./images/images/homer.jpg";
import imageMerge from "./images/images/merge.png";
import imageLisa from "./images/images/lisa.png";
import imageMaggie from ".//images/images/maggie.png";
import imageBart from "./images/images/bart.png";


export default {
  name: "Welcome",
  props: ['members', 'status-admin'],
  data() {
    return {
      loginStatus: false,
      isHidden: false,
      activePersonId: null,
      welcomeHeading: "who's this",
      hideWelcome: false,
      passwordInput :'',
      activePassword: '',
      
      isHiddenButton: true,
      isHiddenHint: true, 
      activeHint: null,
      activeHint: null,
      activePicture: null,
      activeName: null,

      members: [
        {
          name: "Homer",
          backgroundPic: imageHomer,
          id: 0,
          password: "123456",
          hint: "Count your fingers and add one extra :)",
          statusLoginShow: false,
          isSelected: false,
        },
        {
          name: "Merge",
          backgroundPic: imageMerge,
          id: 1,
          password: "maggie",
          hint: "Our daughter's name",
          statusLoginShow: false,
          isSelected: false,
        },
        {
          name: "Lisa",
          backgroundPic: imageLisa,
          id: 2,
          password: "314159",
          hint: "there are numbers which creates a non-integer that you need to count circumference of a circle ",
          statusLoginShow: false,
          isSelected: false,
        },
        {
          name: "Maggie",
          backgroundPic: imageMaggie,
          id: 3,
          password: "pacifier",
          hint: "I 'm crying when it falls out of my mouth",
          statusLoginShow: false,
          isSelected: false,
        },

        {
          name: "Bart",
          backgroundPic: imageBart,
          id: 4,
          password: "eminem",
          hint: "the best american rapper EVER!!",
          statusLoginShow: false,
          isSelected: false,
        },
      ],
    };
  },
  // computed: {
  //   password
  // },
  methods: {
    showLoginBox(personId) {
      this.activePersonId = personId;
      
      
      this.$emit("show-login");
      this.isHidden = true; 
      console.log(personId);
    },
    backLogin() {
      this.$emit("back-login");
      this.isHidden = false;
      this.activePersonId = null;
      
    },
    changeWelcome() {
      if (this.activePersonId = null) {
        this.hideWelcome = false;
      } else if (this.activePersonId = !null){
        this.hideWelcome = true;
      }
    },
    login(){
       if (this.activePersonId === 0) {
      this.$emit("login-homer");
    }
  }
    // login(userPassword){
    //   let  passInput = document.getElementById("user-password");
    //   let  passInputValue = passInput.value;
    //    this.activePassword = userPassword;
    //    let error = document.getElementById("password-error");


       
    //   if (passInputValue == "") {
    //     error.innerText = "no password no entrance!";
    //     this.passInputValue = "";
    //   } else if (passInputValue.length != 6 ) {
    //     error.innerText ="Your password has wrong length, it should be exactly 6 signs, letters or/and numbers. Do you need some help?";
    //     const helpButton = document.getElementById("help-button");
    //     error.appendChild(helpButton)
    //     helpButton.innerText = "yup, help please";
    //     this.isHiddenButton = false;
    //   } else if (this.activePersonId === 0) {
    //     this.$emit("login-homer", {password: userPassword, id: this.activePersonId});
      
    //   } else if (this.activePersonId === 1 && passInputValue === userPassword ){
    //     this.$emit("login-merge", {password: userPassword, id: this.activePersonId});
    //   }
    //    else if (this.activePersonId === 2 && passInputValue === userPassword ){
    //     this.$emit("login-lisa", {password: userPassword, id: this.activePersonId});
    //   }
    //    else if (this.activePersonId === 3 && passInputValue === userPassword ){
    //     this.$emit("login-bart", {password: userPassword, id: this.activePersonId});
    //   }
    //    else if (this.activePersonId === 4 && passInputValue === userPassword ){
    //     this.$emit("login-maggie", {password: userPassword, id: this.activePersonId});
    //   }
      

    // },
    // showHint(activePersonHint){
    //   this.activeHint = activePersonHint;
    //   this.isHiddenHint = false;
    //   console.log(activePersonHint)
    // },
    // editThumbnail(){
    //   this.$emit("edit-thumbnail", {backgroundPic: this.backgroundPic, name: this.name});
   
 


  }
};
</script>

<style>
#help-button {
  background-color: aquamarine;
  color: black;
 
  
}

.button, .user-input {
  padding: 10px;
  margin: 10px; 
}
.back {
  background-color: rgb(208, 122, 165);
}
.button {
  width: 150px;
  border: none;
  color: whitesmoke;
}
.submit {
  background-color: rgb(99, 191, 191);
}
.user-input {
  width: 300px;
}
.form-box {
  top: 50%;
  left: 20%;
  margin-left: auto;
  
  position: absolute;
}
#personForm {
  height: 100%;
  display: flex;
  flex-direction: column;
  align-items: center;

}

.hidden, .hiddenwelcome, .hiddenButton, .hiddenHint {
  visibility: hidden;
}

.family-container {
  padding: 100px;

  margin: 5px;
}

.person {
  display: inline-block;
  width: 20%;
}
.name {
  text-align: center;
  align-content: center;

  font-size: larger;
  font-weight: bolder;
  padding: 30px;
}

.image {
  border-radius: 100%;
  display: inline-block;
  margin-left: 120px;
  margin-right: 120px;

  width: 100px;
  height: 100px;
}
.hvr-float-shadow {
  display: inline-block;
  vertical-align: middle;
  -webkit-transform: perspective(1px) translateZ(0);
  transform: perspective(1px) translateZ(0);
  box-shadow: 0 0 1px rgba(0, 0, 0, 0);
  position: relative;
  -webkit-transition-duration: 0.3s;
  transition-duration: 0.3s;
  -webkit-transition-property: transform;
  transition-property: transform;
}
.hvr-float-shadow:before {
  pointer-events: none;
  position: absolute;
  z-index: -1;
  content: "";
  top: 100%;
  left: 5%;
  height: 10px;
  width: 90%;
  opacity: 0;
  background: -webkit-radial-gradient(
    center,
    ellipse,
    rgba(0, 0, 0, 0.35) 0%,
    rgba(0, 0, 0, 0) 80%
  );
  background: radial-gradient(
    ellipse at center,
    rgba(0, 0, 0, 0.35) 0%,
    rgba(0, 0, 0, 0) 80%
  );

  -webkit-transition-duration: 0.3s;
  transition-duration: 0.3s;
  -webkit-transition-property: transform, opacity;
  transition-property: transform, opacity;
}
.hvr-float-shadow:hover:before,
.hvr-float-shadow:focus:before,
.hvr-float-shadow:active:before {
  opacity: 1;
  -webkit-transform: translateY(5px);
  transform: translateY(5px);
}

.hvr-float-shadow:hover,
.hvr-float-shadow:focus,
.hvr-float-shadow:active {
  -webkit-transform: translateY(-10px);
  transform: translateY(-10px);
  box-shadow: 10px 10px 10px rgba(105, 109, 110, 0.816);
}
</style>
