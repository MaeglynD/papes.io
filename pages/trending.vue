<template>
  <div class="trending-container">
    <div class="trending-bg-container"></div>
    <div class="trending-gradient">
      <h1>Trending</h1>
    </div>
      <section v-if="errored">
          <p>an error happened bro, api is like down or something - tell me on twitter </p>
      </section>
      <section v-else>
        <div v-if="loading" class="lds-ellipsis"><div></div><div></div><div></div><div></div></div>
        <div v-else class="trending-flex">
          <div class="tr-card" v-for='x in info["Backgrounds"]' @click="changeLocal(x.item)">
            <nuxt-link to="/showcase">
            <div class="img-container" :style='{ backgroundImage: "url(" + x.thumb + ")", }'>

            </div>

            <h3>{{ x.name }}</h3></nuxt-link><v-menu  offset-y>
              <v-btn icon slot="activator"><span class="mdi mdi-dots-vertical"></span></v-btn>
              <v-list>
                <v-list-tile @click="diaToggle()">
                  <v-list-tile-title class="body-2">Add to collection</v-list-tile-title>
                </v-list-tile>
              </v-list>
            </v-menu>
            <p>{{ x.creator }}</p>
            <p class="inline">{{ x.views }} </p> <p class="inline"> views</p> <p class=" inline date-added"> &bull; {{ x.date }}</p>
          </div>
      </div>
      </section>
      <v-slide-y-transition mode="out-in">
        <nuxt />
      </v-slide-y-transition>
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
      errored: false

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
    methods: {
      diaToggle(){
        this.$parent.$parent.$parent.dialog = true
        this.$parent.$parent.$parent.tabs = "LOGIN"
        this.$parent.$parent.$parent.tabText = "Sign In"
      },
      changeLocal(y){
        localStorage.setItem("currentImg", y)
      }
    }
}

</script>

<style scoped>

.trending-container{
  width: 100%;
  padding-bottom: 150px;
  background: rgb(18,18,18);
}

.trend-dia-container{
  max-width: 1500px;
}

.trending-bg-container{
  min-height: 350px;
  max-height: 500px;
  height: 20vw;
  background: url("../static/trending-bg.png") bottom center/cover no-repeat;
}
.trending-gradient{
  width: 100%;
  height: 300px;
  margin-top: -300px;
  background: rgb(18,18,18); /* Old browsers */
  background: -moz-linear-gradient(top, rgba(18,18,18,0) 0%, rgba(18,18,18,1) 100%); /* FF3.6-15 */
  background: -webkit-linear-gradient(top, rgba(18,18,18,0) 0%,rgba(18,18,18,1) 100%); /* Chrome10-25,Safari5.1-6 */
  background: linear-gradient(to bottom, rgba(18,18,18,0) 0%,rgba(18,18,18,1) 100%); /* W3C, IE10+, FF16+, Chrome26+, Opera12+, Safari7+ */
}
.trending-gradient h1{
  font-weight: 300;
  font-size: 52px;
  text-align: Center;
  padding-top: 100px;
}
.trending-flex{
  max-width: 1400px;
  margin: auto;
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
}
.tr-card{
  height: 284px;
  flex: 0 336px;
  margin: 0px 7px 32px 0px ;
}
.tr-card:hover .v-btn{
  opacity: 1;
}
.tr-card h3{
  font-size: 16px;
  font-weight: 500;
  margin-top: 10px;
  margin-bottom: 6px;
  display: inline-block;
}
.tr-card .v-menu{
  float: right;
}
.tr-card .v-btn{
  margin-top: 10px;
  color: #888888;
  opacity: 0;
  padding: 0;
  margin-left: 0;
}
.tr-card .v-btn span{
  margin: 0;
}

.tr-card p{
  font-size: 14.5px;
  color: #888888;
  margin-bottom: 0;
}
.img-container{
  width: 100%;
  height: 191px;
  background: darkgrey;
  background-repeat:no-repeat;
  background-size: auto;
  background-position:center;
  transition: 0.2s;
}
.img-container:hover{
  cursor: pointer;
  filter: brightness(120%);
}
.tr-card .inline{
  display: inline-block;
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
@media only screen and (max-width: 380px) {
  .tr-card{
    padding: 2%;
    height: 284px;
    flex: 0 99%;
    margin: 0px 1% 32px 0px ;
  }
  .img-container{
    width: 100%;
    height: 191px;
    background: darkgrey;
    background-position: center center;
    background-repeat: no-repeat;
    background-size: cover;
    -moz-background-size: cover;
    -webkit-background-size: cover;
    transition: 0.2s;
  }
}
@media only screen and (max-height: 700px) {
  .trending-gradient{
    height: 250px;
    margin-top: -250px;
  }
  .trending-gradient h1{
    font-size: 40px;
    padding-top: 65px;
  }
}


</style>
