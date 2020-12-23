<template>
  <div>
    <nav class="navbar navbar-expand-lg navbar-light bg-light">
      <div class="container-fluid">
        <a class="navbar-brand" href="#">
            <img src="../assets/rsz_e-voting_1.png" height="25" alt="">
        </a>
        <!-- <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarSupportedContent" aria-controls="navbarSupportedContent" aria-expanded="false" aria-label="Toggle navigation">
          <span class="navbar-toggler-icon"></span>
        </button> -->
        <!-- <div class="collapse navbar-collapse" id="navbarSupportedContent"> -->
          <ul class="top-navbar ml-auto mb-2 mb-lg-0">
            <li class="">
              <a class="search" href="#">
                  <i class="fas fa-search "></i>
              </a>
            </li>
            <li class="">
              <a v-if="!isLoggedIn" class="btn btn-secondary text-dark login" href="#" data-toggle="modal" data-target="#exampleModalLong">
                <i class="fas fa-user ml-2 mr-2"></i>  Login
              </a>
               <a v-if="isLoggedIn" @click="logout" class="btn btn-secondary text-dark login" href="#">
                <i class="fas fa-user ml-2 mr-2"></i>  Logout
              </a>
            </li>
          </ul>
        <!-- </div> -->
      </div>
    </nav>
    <!-- Hero -->
    <div class="hero-container container-fluid">
         <div class="row top-nav-wrapper">
            <div class="col-lg-10 col-sm-12 col-md-10">
            <ul class="top-navigation">
              <li>
                <a href=""> Election</a>
              </li>
              <li>
                <a href="">Results</a>
              </li>
            </ul>
        </div>
         </div>
    </div>
    <!-- side navigation -->
    <div class="container-fluid">
        <div class="main-container">
          <div class="side-navigation">
             <ul>
               <li><a class=" btn btn-secondary py-2" href="/vote/presidential">Presidential</a></li>
               <li><a class=" btn btn-secondary py-2" href="/vote/vice_president">Vice President</a></li>
               <li><a class=" btn btn-secondary py-2" href="/vote/general_secretary">General Secretary</a></li>
               <li><a class=" btn btn-secondary py-2" href="/vote/financial_secretary">Financial Secretary</a></li>
             </ul>
          </div>
          <div class="vote-content">
              <router-view />
          </div>
        </div>
    </div>

    <!-- modal container -->
    <div class="modal fade" id="exampleModalLong" tabindex="-1" role="dialog" aria-labelledby="exampleModalLongTitle" aria-hidden="true">
      <div class="modal-dialog" role="document">
        <div class="modal-content">
          <div class="modal-header">
            <h5 class="modal-title" id="exampleModalLongTitle">Sign In</h5>
            <button type="button" class="close" data-dismiss="modal" aria-label="Close">
              <span aria-hidden="true">&times;</span>
            </button>
          </div>
          <div class="modal-body">
            <form action="" @submit.prevent="verifyCode" v-if="showNumberInput">
              <div class="row">
                <div class="col-12">
                    <div class="form-group">
                      <label for="number">
                        Enter Phone Number
                      </label>
                      <input type="tel" v-model="phone_number" id="number" class="form-control" required>
                    </div>
                     <div id="get-sign-in-code"></div>
                     <div v-if="error">
                        <p class="alert-danger py-3 pl-3">{{error}}</p>
                      </div>
                      <div class="modal-footer">
                      <!-- <button type="button" class="btn btn-secondary" data-dismiss="modal">Close</button> -->
                      <button  type="submit" class="btn btn-primary" > 
                         <span v-if="isLoading" class="spinner-border spinner-border-sm"></span> Get Sign In Code</button>
                    </div>
                </div>
              </div>
            </form>

            <!-- code input -->
            <form action="" v-if="showCodeInput" @submit.prevent="login">
              <div class="row" >
                <div class="col-md-12">
                    <div class="form-group">
                      <label for="code">Enter Verification Code</label>
                      <input id="code" type="text" class="form-control" v-model="code" required>
                    </div>
                </div>
                 <div v-if="error">
                        <p class="alert-danger py-3 pl-3">{{error}}</p>
                      </div>
              </div>

               <div class="modal-footer">
                      <button type="submit" class="btn btn-primary"> <span v-if="isLoading" class="spinner-border spinner-border-sm"></span> Sign In</button>
                </div>
            </form>

            <!-- error -->
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import firebase from 'firebase/app'


export default {
  name: 'Home',
  data() {
    return {
      topNavActive:false,
      phone_number:'',
      isLoading:false,
      showNumberInput:true,
      showCodeInput:false,
      isLoggedIn: localStorage.getItem('isLoggedIn'),
      code:'',
      error:'',
      success:'',
      users: [
        {
          name:'Adjoa Frimpong',
          title:'Adjoa the leader',
          team: 'Blue team',
          image:require('../assets/imageOne.jpeg')
        },
         {
          name:'Adjoa Frimpong',
          title:'Adjoa the leader',
          team: 'Royal team',
          image:require('../assets/imageTwo.jpeg')
        },
         {
          name:'Adjoa Frimpong',
          title:'Adjoa the leader',
          team: 'Margenta team',
          image:require('../assets/imageThree.jpeg')
        },
         {
          name:'Kofi baboni',
          title:'Adjoa the leader',
          team: 'Gold team',
          image:require('../assets/imageFour.jpeg')
        }
      ]
    }
  },
  methods: {
    logout(){
      localStorage.clear()
      window.location.reload()
    },
    getLoginUser() {
      if(!localStorage.getItem('isLoggedIn')) {
        this.isLoggedIn = false
      }
    },
    login() {
      const self = this
      self.isLoading = true
      self.error = null

      window.confirmationResult.confirm(this.code).then(result => {
        localStorage.setItem('isLoggedIn', true)
        window.location.reload()
      }).catch( error => {
        self.error = "Code Expires try again latter"
        
      })

    },
    verifyCode() {
      const self = this
      self.isLoading = true
      self.error = null

      var appVerifier = window.recaptchaVerifier;
      firebase.auth().signInWithPhoneNumber(`+233${this.phone_number}`, appVerifier)
          .then(function (confirmationResult) {
            window.confirmationResult = confirmationResult;
            self.showNumberInput = false;
            self.isLoading = false;
            self.showCodeInput = true
          }).catch(function (error) {
            console.log()
            self.isLoading = false
            self.error = 'SMS not sent, try again'
            // ...
          });
    }
    
  },

  mounted() {
     const self = this;
      // Start Firebase invisible reCAPTCHA verifier
      window.recaptchaVerifier = new firebase.auth.RecaptchaVerifier('get-sign-in-code')
      recaptchaVerifier.render()
  
  }
}
</script>

<style scoped>
  .top-navbar, .navbar{
    background-color: rgb(253, 250, 250) !important;
    padding:10px 0;
  }
  .top-navbar li{
    display: inline;
    background-color: rgb(253, 250, 250) !important;
  }
  .login{
    background-color:#eee;
    border: 1px solid #4DABF7;  
    text-decoration: none;
    width:130px;
    border-radius: 50px;
    padding: 5px 0;
  }
   .login:hover{
    background-color: #4DABF7;
    border: 1px solid aliceblue; 
  }
  .search{
    color: #4DABF7 !important;
    font-size: 20px;
    margin-right:20px!important;
     background-color: rgb(253, 250, 250) !important;
  }
  .nav-link{
    margin: 10px 0;
  }
  .hero-container{
    background-image: url('../assets/rsz_e-voting.png') ;
    height: 300px;
    background-repeat: no-repeat;
    width:100%;
    background-position: center;
    background-size: cover;
    display: flex;
  }
  .top-navigation{
      list-style: none;
  }
  .top-navigation li {
    display: inline-block;
  }
  .top-navigation ul li {
    width: 200px !important;
  }
  .top-navigation ul li a{
    text-decoration: none;
    background-color: #eee;
    padding:20px 30px;
    text-align: center;
    color:#000
  }
  .top-nav-wrapper{
    position:absolute;
  }
  /* Main container */
  .main-container{
    margin: 50px auto;
    width:80%;
    display: flex;
  }
  .vote-content{
    width:70%
  }
  .side-navigation ul {
    width:30%;
  }
  /* side navigation  */
  .side-navigation ul {
    list-style: none;
  }
  .side-navigation ul li  .btn{
    width:200px ;
    margin:10px 0;
    background-color: rgb(129, 123, 123);
  }
  /* .side-navigation ul li a{
    color:#fff;
    text-decoration: none;
  } */
  .otp-input {
    width: 40px;
    height: 40px;
    padding: 5px;
    margin: 0 10px;
    font-size: 20px;
    border-radius: 4px;
    border: 1px solid rgba(0, 0, 0, 0.3);
    text-align: center;
  }
/* MEDIA QUERIES */
@media screen and (max-width:992px){
  .login{
    margin-right: 10px;
  }
}
</style>