<template>
<div class="row">
   <div class="col-12">
       <div class="row justify-content-center">
           <div class="col-sm-12 col-lg-5" v-for="(user, key) in users" :key="key">
               <div class="card">
                <div class="card">
                        <img class="card-img-top" :src="user.image" alt="Card image cap">
                        <div class="card-body">
                            <h5 class="card-title">{{user.name}}</h5>
                            <p class="card-text">Some quick example text to build on the card title and make up the bulk of the card's content.</p>
                            <a href="#" class="btn btn-primary">Go somewhere</a>
                        </div>
                    </div>
                </div>
           </div>
       </div>
    </div> 
</div>
</template>

<script>
export default {
    data() {
        return {
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

<style>

</style>