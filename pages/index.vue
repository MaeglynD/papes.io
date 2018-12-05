<template>
  <div>
    <div class="main-home-container">
      <v-container grid-list-xs,sm,md,lg,xl class="main-v-cont">
        <v-layout align-center justify-center row fill-height>
          <v-flex xs12 class="main-info">
            <h1 class="">Cross platform, high definition papes from /<span class="glow">wg</span>/</h1>
            <p class="mt-4">We centralize wallpapers of all shapes, sizes and contents so you can browse with <span class="glow">confidence</span>. Anime, nature, winter, summer - you name it we‘ve got it.</p>
          </v-flex>
        </v-layout>
      </v-container>
    </div>
    <v-layout class="main-gradient-container" align-center justify-center row fill-height >
      <span class="mdi mdi-chevron-down  display-1 mt-5" @click="$vuetify.goTo('.main-category-container')"></span>
    </v-layout>
    <div class="main-category-container">
      <v-container grid-list-xs,sm,md,lg,xl class="main-cat-v">
        <h1 class="hidden-sm-and-up text-xs-center mb-4">Browse</h1>
        <v-layout row class=" mb-5">
          <v-flex xs6 hidden-xs-only  align-self-center>
            <h1 class="pa-0 ma-0">Browse</h1>
          </v-flex>
          <v-flex xs12 sm6 class=" control-cont align-self-center">
            <v-btn  class="pa-0 ma-0 right subheading" depressed >ALL</v-btn>
            <div class="main-control-cont">
              <v-btn  :class="{'pa-0': true, 'ma-0': true, 'right': true, 'ml-2': $vuetify.breakpoint.smAndUp, 'mr-4': $vuetify.breakpoint.smAndUp}" depressed ><v-icon>chevron_right</v-icon></v-btn>
              <v-btn  class="pa-0 ma-0 right" disabled  ><v-icon>chevron_left</v-icon></v-btn>
            </div>
          </v-flex>
        </v-layout>
        <div class="main-choose-cont">
          <v-layout align-space-around row justify-center :class="{'wrap': $vuetify.breakpoint.smAndDown, 'fill-height': $vuetify.breakpoint.mdAndUp }">
            <v-flex xs12 sm12 m4 >
              <div class="cat-parent">
                <div class="cat-text">
                  <h2>mood</h2>
                  <span class="mdi mdi-weather-lightning"></span>
                </div>
                <div class="cat-child a">

                </div>
              </div>
            </v-flex>
            <v-flex xs12  sm12 m4 :class="{'mx-4': $vuetify.breakpoint.mdAndUp}">
              <div class="cat-parent">
                <div class="cat-text">
                  <h2>trending</h2>
                  <span class="mdi mdi-fire"></span>
                </div>
                <div class="cat-child b">

                </div>
              </div>
            </v-flex>
            <v-flex xs12 sm12 m4>
              <div class="cat-parent">
                <div class="cat-text">
                  <h2>Seasonal</h2>
                  <span class="mdi mdi-snowflake"></span>
                </div>
                <div class="cat-child c">

                </div>
              </div>
            </v-flex>
          </v-layout>
        </div>
      </v-container>
    </div>
  </div>
</template>


<style scoped>
.main-home-container{
  top: 0;
  height: 100vh;
  width: 100%;
  background: url("../static/rainguy.png") top center/cover no-repeat;
  max-height: 969px;
  min-height: 500px;
}
.main-v-cont{
   max-width: 900px;
   height: 100%;

}
.main-info h1{
  font-size: 60px;
  line-height: 1.3;
  font-weight: 300;
  text-shadow: 3px 4px 5px rgba(0, 0, 0, 0.18);
}
.main-info p{
  max-width: 830px;
  line-height: 1.3;
  font-size:31.5px;
  font-weight: 300;
  color: rgba(255, 255, 255, 0.7);
}
.main-info{
  margin-top: -10%;
}
.main-gradient-container{
  margin-top: -300px;
  width: 100%;
  height: 300px;
  background: rgb(18,18,18); /* Old browsers */
  background: -moz-linear-gradient(top, rgba(18,18,18,0) 0%, rgba(18,18,18,1) 100%); /* FF3.6-15 */
  background: -webkit-linear-gradient(top, rgba(18,18,18,0) 0%,rgba(18,18,18,1) 100%); /* Chrome10-25,Safari5.1-6 */
  background: linear-gradient(to bottom, rgba(18,18,18,0) 0%,rgba(18,18,18,1) 100%); /* W3C, IE10+, FF16+, Chrome26+, Opera12+, Safari7+ */
  filter: progid:DXImageTransform.Microsoft.gradient( startColorstr='#17181a', endColorstr='#17181a',GradientType=0 ); /* IE6-9 */
}
.main-gradient-container span:hover{
  cursor: pointer;
}
.main-category-container{
  height: 100vh;
  min-height: 800px;
  max-height: 969px;
  width: 100%;
  padding-top: 64px;
  background: rgb(18,18,18)
}
.main-cat-v{
  max-width: 1100px;
  height: 100%;
  padding-top: 64px;
}
.main-cat-v h1{
  font-weight: 300;
  font-size: 40px;
}
.main-control-cont .v-btn{
  background-color: rgba(255, 255, 255, 0);
  min-width: 40px;
}
.main-control-cont .v-btn--disabled{
  border: 0px;
  background: #38393a;
}
.control-cont .v-btn{
  height: 45px;
}
.main-choose-cont{
  width: 100%;

  height: 500px;
}
.cat-parent, .cat-child{
  width: 100%;
  height: 100%;
  overflow: hidden;
  transition: 0.4s;
}
.cat-child{
  background-position: center;
  background-size: cover;
  background-repeat: no-repeat;
  filter: brightness(40%);
  margin-top: -500px;
}
.cat-parent .a{
  background-image: url("../static/cat-a.png");
}
.cat-parent .b{
  background-image: url("../static/cat-b.png");
}
.cat-parent .c{
  background-image: url("../static/cat-c.png");
}
.cat-text{
  width: 100%;
  height: 100%;
  position: relative;
  z-index: 1;
  text-align: center;
}
.cat-text h2{
  font-size: 27px;
  font-weight: 300;
  letter-spacing: 7px;
  text-transform: uppercase;
  padding-top: 20px;
  padding-bottom: 40px;
}
.cat-text span{
  font-size: 170px;
}
.cat-child{
}
.cat-parent:hover{
  cursor: pointer;
}
.cat-parent:hover .cat-child, .cat-parent:focus .cat-child{
    transform: scale(1.2);
    filter: brightness(100%);
}
@media only screen and (max-width: 1600px), screen and (max-height: 800px) {
  .main-v-cont{
     max-width: 720px;

  }
  .main-info h1{
    font-size: 48px;

  }
  .main-info p{
    max-width: 664px;
    font-size:25.2px;
  }
}
@media only screen and (max-height: 800px) {
  .main-category-container{
    min-height:740px;
  }
  .main-choose-cont{
    height: 400px;
  }
  .cat-child{
    margin-top: -400px;
  }
  .cat-text span{
    font-size: 130px;
  }
}
@media only screen and (max-width: 960px) {
  .main-category-container{
    height: 1300px;
    max-height: 1300px;
  }
  .main-choose-cont{
    height: 1200px;
  }
  .cat-child{
    background-position: center center;
    background-size: cover;
    background-repeat: no-repeat;
    filter: brightness(40%);
    margin-top: -300px;
  }
  .cat-parent{
    height: 300px;
  }
  .cat-text{
    width: 100%;
    height: 100%;
    position: relative;
    z-index: 1;
    text-align: center;
  }
  .cat-text h2{
    font-size: 27px;
    font-weight: 300;
    letter-spacing: 7px;
    text-transform: uppercase;
    padding-top: 20px;
    padding-bottom: 5px;
  }
  .cat-text span{
    font-size: 130px;
  }
}
@media only screen and (max-height: 700px) {
  .main-info{
    margin-top: 0%;
  }
}
@media only screen and (max-width: 1000px), screen and (max-height: 600px) {
  .main-home-container{
    text-align: center;
  }
  .main-v-cont{
     max-width: 90%;
     padding: 0 20px;

  }
  .main-info p{
    max-width: 100%;
  }
}
@media only screen and (max-width: 700px) {
  .main-info h1{
    font-size: 30px;

  }
  .main-category-container h1{
    font-size: 30px;
  }
  .main-info p{
    font-size:18px;
  }
}
@media only screen and (max-width: 600px) {
  .main-control-cont .v-btn{
    min-width: 33%;
  }
  .control-cont .v-btn{
    width: 33%;
  }
}
@media only screen and (max-width: 350px) {
  .main-info p{
    font-size:16px;
  }
}
</style>
