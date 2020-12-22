<template>
  <div>
    <nav class="navbar navbar-expand-lg navbar-light bg-light">
      <div class="container-fluid">
        <a class="navbar-brand" href="#">
            <img src="../assets/logo.png" height="15" alt="">
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
                <i class="fas fa-user ml-2"></i>  Login
              </a>
            </li>
          </ul>
        </div>
      </div>
    </nav>
  </div>
</template>

<script>

export default {
  name: 'Home',

}
</script>

<style scoped>
  .navbar{
    background-color: #fff !important;
  }
  .login{
    background-color:aliceblue;
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
</style>