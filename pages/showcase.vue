<template>
  <div class="showcase-container">
    <section v-if="errored">
        <p>an error happened bro, api is like down or something - tell me on twitter </p>
    </section>
    <section v-else>
      <div v-if="loading" class="loading-container"><div class="lds-ellipsis"><div></div><div></div><div></div><div></div></div></div>
    <div v-else class="showcase-inner">
      <div class="image-container">
        <v-card flat class="ma-0">
        <v-responsive :aspect-ratio="16/9" class="ma-0" :style='{ backgroundImage: "url(" + info["Backgrounds"][getCurrentImg()].url + ")", }'>
        </v-responsive>
      </v-card>
      <h2>{{ info["Backgrounds"][local].name }}</h2>
      <p>{{ info["Backgrounds"][local].views }} views</p>
      <div class="btn-container">
        <v-tooltip top><v-btn slot="activator" flat><span class="mdi mdi-heart"> </span><div> {{ info["Backgrounds"][local].likes }}</div></v-btn>Like</v-tooltip>
        <v-tooltip top><v-btn slot="activator" flat><span class="mdi mdi-heart-off"></span><div>{{ info["Backgrounds"][local].dislikes }}</div></v-btn>Dislike</v-tooltip>
        <v-tooltip top><v-btn slot="activator" flat><span class="mdi mdi-cloud-download"></span><div>1K</div></v-btn>Download</v-tooltip>
        <v-tooltip top><v-btn slot="activator" flat class="report"><span class="mdi mdi-flag"></span><div>REPORT</div></v-btn>Report Image</v-tooltip>
      </div>
      <div class="hr"></div>
      <div class="user-container">

        <div class="profile-icon" :style='{ backgroundImage: "url(https://randomuser.me/api/portraits/med/women/" + Math.floor(Math.random() * 99)  + ".jpg)", }'></div>
        <h4>{{ info["Backgrounds"][local].creator }}</h4><br>
        <p>Submitted {{ info["Backgrounds"][local].date }}</p>
        <p class="desc">{{ info["Backgrounds"][local].desc }} </p>

      </div>

        <div class="hr"></div>
      </div>
      <div class="also-container">
        <h3>You also might like</h3>
        <div class="recommendation">

          <div class="rec-container" @click="sidebarImg(randInt)" >
            <v-card flat class="ma-0">
            <v-responsive :aspect-ratio="16/9" class="ma-0" :style='{ backgroundImage: "url(" + info["Backgrounds"][getRandInt()].url + ")", }'>

            </v-responsive>
            </v-card>
          <div class="rec-text">
            <h3>{{ info["Backgrounds"][randInt].name }}</h3>
            <p>{{ info["Backgrounds"][randInt].creator }}</p>
            <p>{{ info["Backgrounds"][randInt].views}} views</p>
          </div>
        </div>

        </div>
        <div class="hr-also"></div>

        <div class="rec-container" v-for="x in 10" @click="sidebarImg(x)">
          <v-card class="ma-0">
          <v-responsive :aspect-ratio="16/9" class="ma-0" :style='{ backgroundImage: "url(" + info["Backgrounds"][x].url + ")", }'>

          </v-responsive>
          </v-card>
        <div class="rec-text">
          <h3>{{ info["Backgrounds"][x].name }}</h3>
          <p>{{ info["Backgrounds"][x].creator }}</p>
          <p>{{ info["Backgrounds"][x].views}} views</p>
        </div>
      </div>


      </div>
    </div>
  </section>
  <nuxt />
  </div>

</template>
<script>

  import axios from 'axios';

  export default {
    name: 'App',
    data () {
      return {
        info: null,
        loading: true,
        errored: false,
        local: 0,
        randInt: 0
      }

    },

    // Fetches posts when the component is created.
    created () {
      axios
        .get('https://papesio.github.io/images.json')
        .then(response => {
          this.info = response.data
        })
        .catch(error => {
          console.log(error)
          this.errored = true
        })
        .finally(() => this.loading = false)

    },
    methods:{
      getCurrentImg(){
      this.local = localStorage.getItem('currentImg')
      return localStorage.getItem('currentImg')
    },
    getRandInt(){
      this.randInt = Math.floor(Math.random() * 10) + 10
      return this.randInt
    },
    sidebarImg(y){
      localStorage.setItem("currentImg", y)
      window.scroll(0,0)
      this.$router.go()
    }

  }
}

</script>

<style scoped>
  .showcase-container{
    width: 100%;
    background: rgb(18,18,18);
    padding-bottom: 200px;
    padding-right: 10px;
  }
  .showcase-inner{
    max-width: 1700px;
    margin: auto;
    margin-top: 60px;
  }
  .image-container{
    width: calc(100% - 424px);
    display: inline-block;
    float: left;
    margin-left: 34px;
    padding-top: 24px;
    padding-right: 24px;
  }

  .image-container h2{
    font-size: 20px;
    font-weight: 400;
    margin-top: 13px;
    margin-bottom: 9px;
  }
  .image-container p {
    font-size: 17px;
    color: #888888;
    display: inline-block;
  }
  .also-container{
    height: 1000px;
    width: 390px;
    display: inline-block;
    padding-top: 24px;


  }
  .image-container .btn-container{
    display: inline-block;
    float: right;
    padding-right: 10px;
    margin-top: -5px;
  }
  .image-container .btn-container .v-btn{
    font-size: 14px;
    font-weight: 400;
    margin: 0;
    color: #888888;
  }
  .image-container .btn-container .v-btn:before{
    background: none;

  }
  .image-container .btn-container .v-btn:hover{
    color: #f3c669;

  }
  .image-container .btn-container .v-btn span{
    margin-right: 3px;
  }
  .img-showcase{
    width: 100%;
    background: grey;
  }

  .hr{
    margin-top: 10px;
    width: 100%;
    height: 1px;
    background: #888888;
    opacity: 0.3;
  }
  .also-container h3{
    font-size: 16px;
    font-weight: 400;
    margin-bottom: 10px;
  }
  .also-container .v-card{
    width: 190px;
    display: inline-block;
    float: left;
  }
  .rec-container:hover .v-card .v-responsive{
    filter: brightness(115%);
    cursor:pointer;
  }
  .rec-container .v-card .v-responsive{
    transition: 0.2s;
  }
  .image-container .v-card .v-responsive{
    background-repeat:no-repeat;
    background-size: contain;
    background-position:center;
  }
  .also-container .v-card .v-responsive{
    background-repeat:no-repeat;
    background-size: 200px 120px ;
    background-position:center;
  }
  .theme--dark.v-card {
      background-color: rgba(0,0,0,0.3);
      border:0;
      color: #fff;
  }


  .rec-text{
    width: calc(100% - 198px);
    display: inline-block;
    margin-left: 8px;
  }
  .rec-text h3{
    margin-bottom: 0;
  }
  .rec-text p{
    margin: 0;
    color: #888888;
  }
  .also-container .hr-also{
    width: 100%;
    height: 1px;
    background: #888888;
    opacity: 0.3;
    margin: 20px 0px;
  }
  .recommendation{
    min-height: 107px;
  }
  .rec-container{
    min-height: 107px;
    display: block;
    margin-top: 10px;
  }
  .loading-container{
    height: 100vh;
    width: 100vw;
    padding-top: 40vh;
  }
  .user-container .profile-icon{
    margin-top: 20px;
    display: inline-block;
    width: 48px;
    height: 48px;
    border-radius: 50%;
    float: left;
    background-repeat:no-repeat;
    background-size: cover;
    background-position:center;
  }
  .user-container h4{
    font-weight: 400;
    display: inline-block;
    margin: 0;
    margin-left: 15px;
    margin-top: 25px;
    font-size: 15px;
  }
  .user-container p{
    margin-left: 14px;
    font-size: 14px;
  }
  .user-container .desc{
    font-size: 15px;
    color: white;
    display: block;
    max-width: 500px;
    margin-left: 65px;
    font-weight: 400;
    margin-bottom: 25px;
  }
  .lds-ellipsis {
    margin: auto;
    display: block;
    position: relative;
    width: 64px;
    height: 64px;
  }
  .lds-ellipsis div {
    position: absolute;
    top: 27px;
    width: 11px;
    height: 11px;
    border-radius: 50%;
    background: #fff;
    animation-timing-function: cubic-bezier(0, 1, 1, 0);
  }
  .lds-ellipsis div:nth-child(1) {
    left: 6px;
    animation: lds-ellipsis1 0.6s infinite;
  }
  .lds-ellipsis div:nth-child(2) {
    left: 6px;
    animation: lds-ellipsis2 0.6s infinite;
  }
  .lds-ellipsis div:nth-child(3) {
    left: 26px;
    animation: lds-ellipsis2 0.6s infinite;
  }
  .lds-ellipsis div:nth-child(4) {
    left: 45px;
    animation: lds-ellipsis3 0.6s infinite;
  }
  @keyframes lds-ellipsis1 {
    0% {
      transform: scale(0);
    }
    100% {
      transform: scale(1);
    }
  }
  @keyframes lds-ellipsis3 {
    0% {
      transform: scale(1);
    }
    100% {
      transform: scale(0);
    }
  }
  @keyframes lds-ellipsis2 {
    0% {
      transform: translate(0, 0);
    }
    100% {
      transform: translate(19px, 0);
    }
  }

  @media only screen and (max-width: 1015px) {
    .showcase-container{
      padding-right: 0px;
    }
    .image-container{
      width: 95%;
      display: block;
      float: none;
      padding: 0;
      margin: 0;
      margin: auto;
      margin-top: 1%;
    }
    .img-showcase{
      width: 100%;
      background: grey;
    }
    .also-container{
      padding: 0;
      margin: 0;
      width: 95%;
      display: block;
      margin: auto;
      margin-top: 20px;

    }
  }
  @media only screen and (max-width: 660px) {
    .image-container .btn-container{
      display: block;
      float: none;
      width: 100%;
      font-size: 10px;
    }
    .image-container .btn-container .v-btn{
      width: 24%;
    }
  }
  @media only screen and (max-width: 420px) {
    .also-container .v-card{
      width: 140px;
    }
    .rec-text{
       width: calc(100% - 148px)
    }
    .rec-text h3{
      font-size: 14px
    }
    .rec-text p{
      font-size: 12px;
    }
    .rec-container, .recommendation{
      min-height: 80px;
    }
    .image-container .btn-container .report{
      display: none;

    }
    .image-container .btn-container .v-btn{
      width: 32%;

    }
  }
</style>
