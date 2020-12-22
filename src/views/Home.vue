<template>
  <div>
    <nav class="navbar navbar-expand-lg navbar-light bg-light">
      <div class="container-fluid">
        <a class="navbar-brand" href="#">
            <img src="../assets/rsz_e-voting_1.png" height="25" alt="">
        </a>
        <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarSupportedContent" aria-controls="navbarSupportedContent" aria-expanded="false" aria-label="Toggle navigation">
          <span class="navbar-toggler-icon"></span>
        </button>
        <div class="collapse navbar-collapse" id="navbarSupportedContent">
          <ul class="navbar-nav ml-auto mb-2 mb-lg-0">
            <li class="nav-item">
              <a class="nav-link active search" aria-current="page" href="#">
                  <i class="fas fa-search "></i>
              </a>
            </li>
            <li class="nav-item">
              <a class="nav-link login" href="#">
                <i class="fas fa-user ml-2 mr-2"></i>  Login
              </a>
            </li>
          </ul>
        </div>
      </div>
    </nav>
    <!-- Hero -->
    <div class="hero-container container-fluid">
         <!-- <div class="row top-nav-wrapper">
            <div class="col-lg-10 col-sm-12 col-md-10">
            <ul class="top-navigation">
              <li>
                <a href=""> Core Members</a>
              </li>
              <li>
                <a href="">Auxilliary Members</a>
              </li>
            </ul>
        </div>
         </div> -->
    </div>
    <!-- side navigation -->
    <div class="container-fluid">
        <div class="main-container">
          <div class="side-navigation">
             <ul>
               <li><a href="">Presidential</a></li>
               <li><a href="">Vice President</a></li>
               <li><a href="">General Secretary</a></li>
               <li><a href="">Financial Secretary</a></li>
             </ul>
          </div>
        </div>
    </div>
  </div>
</template>

<script>

export default {
  name: 'Home',
  data() {
    return {
      topNavActive:false,
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
  }
}
</script>

<style scoped>
  .navbar{
    background-color: rgb(253, 250, 250) !important;
  }
  .login{
    background-color:#eee;
    border: 1px solid #4DABF7;  
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
  }

  /* side navigation  */
  .side-navigation ul {
    list-style: none;
  }
  .side-navigation ul li {
    width:200px ;
    margin:10px 0;
    padding:10px 20px;
    background-color: rgb(129, 123, 123);
    border-radius: 10px ;
    cursor: pointer;
  }
  .side-navigation ul li a{
    color:#fff;
    text-decoration: none;
  }
</style>