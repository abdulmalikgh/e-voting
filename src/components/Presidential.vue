<template>
<div class="row mb-5">
   <div class="col-12 ">
       <div class="row justify-content-center">
           <div class="col-12">
               <h2 class="text-center">Presidential Election</h2>
               <p class="text-center">Select candidate and continue to cast your vote</p>
           </div>
           <div class="col-sm-8 col-xs-10 col-lg-5" v-for="(user, key) in users" :key="key" @mouseover="getSelectedCandidate(user, key)">  
                <div class="card top-card" >
                    <div class="setOverlay">
                        <a class="btn btn-outline-light px-5 py-2" href="#selected">Select</a>
                    </div>
                    <img class="" height="220" :src="user.image" alt="Card image cap">
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
       <div class="row justify-content-center" v-if="showCandidate" id="selected">
           <div class="col-sm-8 col-xs-10 col-lg-5">
               <div class="card">
                   <div class="overlay">
                       <div class="mb-3 text-light">
                           <i class="fas fa-fingerprint" style="font-size:120PX"></i>
                       </div>
                       <button v-if="!isLoading" class="btn btn-outline-light px-5 px-2" @click="submitVote(seectedCandidtae)">
                           Vote
                       </button>
                       <button v-if="isLoading" class="btn btn-outline-light px-5 px-2">
                           <span class="spinner-border spinner-border-sm"></span>...submitting
                       </button>
                   </div>
                    <img class="img-fluid" :src="seectedCandidtae.image" alt="Card image cap">
                    <div class="card-body">
                        <h5 class="card-title">{{seectedCandidtae.name}}</h5>
                        <p class="card-text">{{seectedCandidtae.title}}</p>
                    </div>
                    <div class="card-footer text-light" :style="`background-color:${seectedCandidtae.color}`">
                        {{seectedCandidtae.team}}
                    </div>
                </div>
           </div>
       </div>
    </div> 
</div>
</template>

<script>
import toasterMixin from '../mixins/toastermixin'

const $ = require('jquery')
export default {
    data() {
        return {
              seectedCandidtae:{},
              showCandidate:false,
              isLoading: false,
              key:null,
        users: [
        {
          name:'Adjoa Frimpong',
          title:'Adjoa the leader',
          team: 'Blue team',
          image:require('../assets/imageOne.jpeg'),
          color:'blue',
          vote_name: 'adjoa'
        },
         {
          name:'Kofi Mensah',
          title:'Adjoa the leader',
          team: 'Royal team',
          image:require('../assets/imageTwo.jpeg'),
          color:'#581845 ',
          vote_name:'kofi'
        },
         {
          name:'Abdul-Malik Musah',
          title:'Adjoa the leader',
          team: 'Margenta team',
          image:require('../assets/imageThree.jpeg'),
          color:'#C70039 ',
          vote_name:'malik'
        },
         {
          name:'Owusu Bismark',
          title:'Adjoa the leader',
          team: 'Gold team',
          image:require('../assets/imageFour.jpeg'),
          color:'gold',
          vote_name:'owusu'
        }
      ]
    }
    },
    methods: {
        submitVote(data) {
            const self = this
            this.isLoading = true
            const user = localStorage.getItem('loginUser')
            const vote = data.vote_name
            const presidents = JSON.parse(localStorage.getItem('presidents'))
            
            // keeping track of voters

            if(!localStorage.getItem('voters')) {
                localStorage.setItem('voters',JSON.stringify([user]))
            } else {
                const oldVoters = JSON.parse(localStorage.getItem('voters'))
                const newArray = [user]
                if(!oldVoters.find(number => number == user)) {
                    alert(`You can't vote more than one`)
                    return
                }
                const newVoters = [...oldVoters,...newArray]
                localStorage.setItem('voters', JSON.stringify(newVoters))
              
                // ADDING NEW DATA TO DATABASE
                for(let i = 0; i <= presidents.length; i++) {
                    if(i === this.key) {
                        presidents[i].votes += 1
                    }
                }
                localStorage.setItem('presidents',JSON.stringify(presidents))
                setTimeout(function(){
                    self.isLoading = false;
                     self.toast({
                        message:'Vote submitted successfully.',
                        type:'success'
                    })
                },5000)
               

            }
    

            
        },
        getSelectedCandidate(user, key) {
            this.seectedCandidtae = user
            this.key = key
            this.showCandidate = true

        //        var sizeTheOverlays = function() {
        //     $(".overlay").resize().each(function() {
        //     var h = $(this).parent().outerHeight();
        //     var w = $(this).parent().outerWidth();
        //     $(this).css("height", h);
        //     $(this).css("width", w);
        //         });
        //         };

        // sizeTheOverlays();


        // var width = $(window).width();
        // $(window).resize(function(){
        // if($(this).width() != width){
        //     width = $(this).width();
        //     sizeTheOverlays();
        // }
        // });
         }
    },
    mounted() {
        $(".top-card").hover(
            function () {
                $(this).children(".setOverlay").addClass('overlay');
            }, 
            function () {   
                $(this).children(".setOverlay").removeClass('overlay');
            }
            );

        const data = [
         {
          name:'Adjoa Frimpong',
          title:'Adjoa the leader',
          team: 'Blue team',
          image:require('../assets/rsz_imageone.jpg'),
          color:'blue',
          vote_name:'adjoa',
          votes:0
        },
         {
          name:'Kofi Mensah',
          title:'Adjoa the leader',
          team: 'Royal team',
          image:require('../assets/rsz_imagetwo.jpg'),
          color:'#581845 ',
          vote_name:'kofi',
          votes:0
        },
         {
          name:'Abdul-Malik Musah',
          title:'Adjoa the leader',
          team: 'Margenta team',
          image:require('../assets/rsz_imagefour.jpg'),
          color:'#C70039 ',
          vote_name:'malik',
          votes:0
        },
         {
          name:'Owusu Bismark',
          title:'Adjoa the leader',
          team: 'Gold team',
          image:require('../assets/imageFour.jpeg'),
          color:'gold',
          vote_name:'owusu',
          votes:0
          }
      ]  
      if(!localStorage.getItem('presidents')) {
          localStorage.setItem('presidents', JSON.stringify(data))
      }

    }
}
</script>


<style lang="scss">
    .card{
        border-radius:20px;
        box-shadow: 4px 4px solid #000;
        height: 400px;
        margin-top:20px;
    }
    .card:hover{
     cursor: pointer;
    }
    .card-footer{
        border-bottom-right-radius: 20px !important;
        border-bottom-left-radius: 20px !important;
    }
    img{
        border-top-left-radius: 20px;
        border-top-right-radius: 20px;
    }
    .overlay {  
        display:flex;
        flex-direction: column;
        justify-content: center;
        align-items: center;
        position: absolute;
        height: 100%;
        width:100%;
        z-index: 2;
        background: rgba(39, 42, 43, 0.8);
        transition: opacity 200ms ease-in-out;
        border-radius: 4px;
        opacity: 1;
        border-radius: 20px;
    
        }
</style>