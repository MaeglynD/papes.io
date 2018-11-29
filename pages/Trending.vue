<template>
  <div class="trending-container">
    <div class="trending-bg-container"></div>
    <div class="trending-gradient">
      <h1>Trending</h1>
    </div>
    <div class="trending-flex">
        <div class="trend-dia-container">
          <v-dialog v-model="dialogImage" min-width="400px" max-width="1200px" width="auto"  class="" transition="dialog-transition"  >
            <v-img :src="currentImg" class="ma-3"></v-img>
          </v-dialog>
        </div>
      <div class="tr tr0">
        <div class="showcase-badge"><span class="mdi mdi-fire"></span></div>
        <div class="showcase-cont">
          <div class="showcase-hover" @click="changeDiaImg(0)">
            <span class="mdi mdi-fullscreen"></span>
            <p>Click to enlarge</p>
          </div>
        </div>
        <div class="showcase-btns">
          <v-btn outline :class="{'ma-0': true, 'heart-active': heartState[0] }" @click="toggleHeart(0)"><span class="mdi mdi-heart pr-2"></span>{{ heartArr[0] }}</v-btn>
          <v-btn outline class="ma-0 px-2 ml-2 download" download :href="dlCurrentImg(0)"><span class="mdi mdi-download"></span></v-btn>

          <p class="glow">#1</p>
        </div>
      </div>

      <div class="tr tr1">
        <div class="showcase-cont">
          <div class="showcase-hover" @click="changeDiaImg(1)">
            <span class="mdi mdi-fullscreen"></span>
            <p>Click to enlarge</p>
          </div>
        </div>
        <div class="showcase-btns">
          <v-btn outline :class="{'ma-0': true, 'heart-active': heartState[1] }" @click="toggleHeart(1)"><span class="mdi mdi-heart pr-2"> </span> {{ heartArr[1] }}</v-btn>
          <v-btn outline class="ma-0 px-2 ml-2 download" download :href="dlCurrentImg(1)"><span class="mdi mdi-download"></span></v-btn>

          <p>#2</p>
        </div>
      </div>

      <div class="tr tr2">
        <div class="showcase-cont">
          <div class="showcase-hover" @click="changeDiaImg(2)">
            <span class="mdi mdi-fullscreen"></span>
            <p>Click to enlarge</p>
          </div>
        </div>
        <div class="showcase-btns">
          <v-btn outline :class="{'ma-0': true, 'heart-active': heartState[2] }" @click="toggleHeart(2)"><span class="mdi mdi-heart pr-2"> </span> {{ heartArr[2] }}</v-btn>
          <v-btn outline class="ma-0 px-2 ml-2 download" download :href="dlCurrentImg(2)"><span class="mdi mdi-download"></span></v-btn>

          <p>#3</p>
        </div>
      </div>

      <div class="tr tr3">
        <div class="showcase-cont">
          <div class="showcase-hover" @click="changeDiaImg(3)">
            <span class="mdi mdi-fullscreen"></span>
            <p>Click to enlarge</p>
          </div>
        </div>
        <div class="showcase-btns">
          <v-btn outline :class="{'ma-0': true, 'heart-active': heartState[3] }" @click="toggleHeart(3)"><span class="mdi mdi-heart pr-2"> </span> {{ heartArr[3] }}</v-btn>
          <v-btn outline class="ma-0 px-2 ml-2 download" download :href="dlCurrentImg(3)"><span class="mdi mdi-download"></span></v-btn>

          <p>#4</p>
        </div>
      </div>

      <div class="tr tr4">
        <div class="showcase-cont">
          <div class="showcase-hover" @click="changeDiaImg(4)">
            <span class="mdi mdi-fullscreen"></span>
            <p>Click to enlarge</p>
          </div>
        </div>
        <div class="showcase-btns">
          <v-btn outline :class="{'ma-0': true, 'heart-active': heartState[4] }" @click="toggleHeart(4)"><span class="mdi mdi-heart pr-2"> </span> {{ heartArr[4] }}</v-btn>
          <v-btn outline class="ma-0 px-2 ml-2 download"  download :href="dlCurrentImg(4)"><span class="mdi mdi-download"></span></v-btn>

          <p>#5</p>
        </div>
      </div>

      <div class="tr tr5">
        <div class="showcase-cont">
          <div class="showcase-hover" @click="changeDiaImg(5)">
            <span class="mdi mdi-fullscreen"></span>
            <p>Click to enlarge</p>
          </div>
        </div>
        <div class="showcase-btns">
          <v-btn outline :class="{'ma-0': true, 'heart-active': heartState[5] }" @click="toggleHeart(5)"><span class="mdi mdi-heart pr-2"> </span> {{ heartArr[5] }}</v-btn>
          <v-btn outline class="ma-0 px-2 ml-2 download" download :href="dlCurrentImg(5)"><span class="mdi mdi-download"></span></v-btn>

          <p>#6</p>
        </div>
      </div>

      <div class="tr tr6">
        <div class="showcase-cont">
          <div class="showcase-hover" @click="changeDiaImg(6)">
            <span class="mdi mdi-fullscreen"></span>
            <p>Click to enlarge</p>
          </div>
        </div>
        <div class="showcase-btns">
          <v-btn outline :class="{'ma-0': true, 'heart-active': heartState[6] }" @click="toggleHeart(6)"><span class="mdi mdi-heart pr-2"> </span> {{ heartArr[6] }}</v-btn>
          <v-btn outline class="ma-0 px-2 ml-2 download" download :href="dlCurrentImg(6)"><span class="mdi mdi-download"></span></v-btn>

          <p>#7</p>
        </div>
      </div>

      <div class="tr tr7">
        <div class="showcase-cont">
          <div class="showcase-hover" @click="changeDiaImg(7)">
            <span class="mdi mdi-fullscreen"></span>
            <p>Click to enlarge</p>
          </div>
        </div>
        <div class="showcase-btns">
          <v-btn outline :class="{'ma-0': true, 'heart-active': heartState[7] }" @click="toggleHeart(7)"><span class="mdi mdi-heart pr-2"> </span> {{ heartArr[7] }}</v-btn>
          <v-btn outline class="ma-0 px-2 ml-2 download" download :href="dlCurrentImg(7)"><span class="mdi mdi-download"></span></v-btn>

          <p>#8</p>
        </div>
      </div>

      <div class="tr tr8">
        <div class="showcase-cont">
          <div class="showcase-hover" @click="changeDiaImg(8)">
            <span class="mdi mdi-fullscreen"></span>
            <p>Click to enlarge</p>
          </div>
        </div>
        <div class="showcase-btns">
          <v-btn outline :class="{'ma-0': true, 'heart-active': heartState[8] }" @click="toggleHeart(8)"><span class="mdi mdi-heart pr-2"> </span> {{ heartArr[8] }}</v-btn>
          <v-btn outline class="ma-0 px-2 ml-2 download" download :href="dlCurrentImg(8)"><span class="mdi mdi-download"></span></v-btn>

          <p>#9</p>
        </div>
      </div>


    </div>
  </div>
</template>

<script>

export default {
  name: 'App',
  data () {
    return {
      heartState: [false,false,false,false,false,false,false,false,false],
      heartArr: [327, 288, 259, 191, 163, 140, 99, 78, 75],
      dialogImage: false,
      currentImg: ""
    }
  },
  methods: {
    changeDiaImg(x){
      this.dialogImage = true
      this.currentImg = require('../static/large/t-' + x + '.jpg')
    },
    toggleHeart(x){
      this.heartState[x] = !this.heartState[x]
      if(this.heartState[x] == true){
        this.heartArr.splice(x, 1, this.heartArr[x]+1)
      }else{
        this.heartArr.splice(x, 1, this.heartArr[x]-1)
      }
    },
    dlCurrentImg(x){
      return require('../static/large/t-' + x + '.jpg')
    }
  }
}

</script>

<style scoped>

.trending-container{
  width: 100%;
  padding-bottom: 150px;
}

.trend-dia-container{
  max-width: 1500px;
}

.trending-bg-container{
  min-height: 300px;
  max-height: 500px;
  height: 20vw;
  background: url("../static/trending-bg.png") bottom center/cover no-repeat;
}
.trending-gradient{
  width: 100%;
  height: 300px;
  margin-top: -300px;
  background: rgb(23,24,26); /* Old browsers */
  background: -moz-linear-gradient(top, rgba(23,24,26,0) 0%, rgba(23,24,26,1) 100%); /* FF3.6-15 */
  background: -webkit-linear-gradient(top, rgba(23,24,26,0) 0%,rgba(23,24,26,1) 100%); /* Chrome10-25,Safari5.1-6 */
  background: linear-gradient(to bottom, rgba(23,24,26,0) 0%,rgba(23,24,26,1) 100%); /* W3C, IE10+, FF16+, Chrome26+, Opera12+, Safari7+ */
}
.trending-gradient h1{
  font-weight: 300;
  font-size: 52px;
  text-align: Center;
  padding-top: 100px;
}
.trending-flex{
  max-width: 1100px;
  margin: auto;
  display: -ms-flexbox;
  display: -webkit-flex;
  display: flex;
  flex-flow: row wrap;
  justify-content: center;
  margin-top: -10px;
}
 .trending-flex .tr{
   height: 202px;
   flex: 0 1 280px;
   margin: 17.5px;
   background-color: rgba(53,53,53, 0.69);
   box-shadow: 0px 9px 18px 0px rgba(0, 0, 0, 0.43);
   border-radius: 5px;
   transition: 0.2s;
   padding:  7px;
}
.trending-flex .tr:hover{
  box-shadow: 0px 9px 18px 10px rgba(0, 0, 0, 0.43);
}
.trending-container .trending-flex .showcase-hover{
  width: 100%;
  height: 100%;
  opacity: 0;
  transition: 0.2s;
  background: rgba(0,0,0,0.7);
  color: rgba(255, 255, 255, 0.7);
  text-align: center;
  padding-top: 30px;
}
.showcase-hover span{
  font-size: 30px;
}
.trending-flex .tr .showcase-cont{
  height: 145px;
  padding: 0;
  margin-bottom: 7px;

}
.trending-flex .tr0 .showcase-cont{
  background: url("../static/thumb/t-0.png") bottom center/cover no-repeat;
}
.trending-flex .tr1 .showcase-cont{
  background: url("../static/thumb/t-1.png") bottom center/cover no-repeat;
}
.trending-flex .tr2 .showcase-cont{
  background: url("../static/thumb/t-2.png") bottom center/cover no-repeat;
}
.trending-flex .tr3 .showcase-cont{
  background: url("../static/thumb/t-3.png") bottom center/cover no-repeat;
}
.trending-flex .tr4 .showcase-cont{
  background: url("../static/thumb/t-4.png") bottom center/cover no-repeat;
}
.trending-flex .tr5 .showcase-cont{
  background: url("../static/thumb/t-5.png") bottom center/cover no-repeat;
}
.trending-flex .tr6 .showcase-cont{
  background: url("../static/thumb/t-6.png") bottom center/cover no-repeat;
}
.trending-flex .tr7 .showcase-cont{
  background: url("../static/thumb/t-7.png") bottom center/cover no-repeat;
}
.trending-flex .tr8 .showcase-cont{
  background: url("../static/thumb/t-8.png") bottom center/cover no-repeat;
}


.showcase-cont:hover .showcase-hover{
  opacity: 1;
  cursor: pointer;
}
.showcase-btns .v-btn{
  opacity: 0.8;
  border: 0;
  color: #0d0d0e;
  font-size: 16px;
  font-weight: 400;
}
.showcase-btns .v-btn:hover{
  opacity: 1;
}
.showcase-btns .v-btn.download{
  min-width: 10px;
}
.showcase-btns .v-btn:before{
  background: rgba(255, 255, 255, 1);
}
.showcase-btns span{
  font-size: 20px;
}
.showcase-btns .heart-active{
  color: #f3c669;
}
.showcase-btns p{
  display: inline-block;
  float: right;
  font-size: 17px;
  font-weight: 300;
  margin-top: 5px;
  margin-right: 5px;
  color: rgba(255, 255, 255, 0.3);
}
.showcase-badge{
  height: 50px;
  width: 50px;
  border-radius: 50%;
  background-color: #f8a3a3;
  position: absolute;
  margin-left: -25px;
  margin-top: -25px;
  z-index: 3;
  text-align: center;
  font-size: 33px;
}
.showcase-badge span{
  font-size: 30px;
}
</style>
