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
                            <p class="card-text">{{user.title}}</p>
                        </div>
                        <div class="card-footer text-light" :style="`background-color:${user.color}`">
                            {{user.team}}
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
          image:require('../assets/imageOne.jpeg'),
          color:'blue'
        },
         {
          name:'Adjoa Frimpong',
          title:'Adjoa the leader',
          team: 'Royal team',
          image:require('../assets/imageTwo.jpeg'),
          color:'#581845 '
        },
         {
          name:'Adjoa Frimpong',
          title:'Adjoa the leader',
          team: 'Margenta team',
          image:require('../assets/imageThree.jpeg'),
          color:'#C70039 '
        },
         {
          name:'Kofi baboni',
          title:'Adjoa the leader',
          team: 'Gold team',
          image:require('../assets/imageFour.jpeg'),
          color:'gold'
        }
      ]
    }
    }
}
</script>

<style>

</style>