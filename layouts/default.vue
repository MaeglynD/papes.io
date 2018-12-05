<template>
  <v-app dark>
    <v-toolbar clipped-left id="toolbar"  flat fixed :class="{'toolbar-scroll': scrollPosition}">
      <v-toolbar-side-icon @click="drawer = !drawer"></v-toolbar-side-icon>
      <v-toolbar-title><router-link to="/">papes<span class="glow">.</span>io</router-link></v-toolbar-title>

      <v-card class="input-card hidden-xs-only" hover flat color="rgba(255, 255, 255, 0.15)" height="40px" >
        <v-text-field placeholder="Search" id="search-bar" ref="searchBar" height="40px" class="ma-0 pa-0"> </v-text-field>
      </v-card>
      <v-spacer></v-spacer>

      <v-dialog v-model="dialog" class="dialog-container" height="675px" width="450px" transition="slide-y-transition">
      <v-btn dark color="rgba(255, 255, 255, 0)" large depressed class="toolbtn" slot="activator" @click="changeDiaClassLogin()"><span class="hidden-lg-and-up"><span class="mdi mdi-login"></span></span><span class="hidden-md-and-down">sign in</span></v-btn>
      <v-btn dark color="rgba(255, 255, 255, 0)" large depressed class="toolbtn create-acc" slot="activator" @click="changeDiaClassCreate()"><span class="hidden-lg-and-up"><span class="mdi mdi-account-plus"></span></span><span class="hidden-md-and-down">create account</span></v-btn>

      <v-card class="dialog-account">
        <v-card class="dialog-top" color="rgba(0,0,0,0)" flat >
          <v-layout row wrap>
            <v-flex xs1>
              <v-btn icon large  class="title " @click="dialog = false"><v-icon>close</v-icon></v-btn>
            </v-flex>
            <v-flex xs10>
              <v-card-text center class="tab-title">
                {{ tabText }}
              </v-card-text>
            </v-flex>
          </v-layout>
        </v-card>
        <v-layout row wrap class="px-4">
          <v-flex>
            <v-tabs v-model="tabs" color="transparent" slider-color="primary" centered grow slot="extension" >
              <v-tabs-slider color="primary"></v-tabs-slider>
              <v-tab href="#CREATE" @click="tabText = 'Create Account'">
                <span class="mdi mdi-account-plus"></span>
              </v-tab>
              <v-tab href="#LOGIN" @click="tabText = 'Sign In'">
                <span class="mdi mdi-login"></span>
              </v-tab>
              <v-tab href="#FORGOT" @click="tabText = 'Reset Password'">
                <span class="mdi mdi-key-variant"></span>
              </v-tab>
            </v-tabs>
          </v-flex>
          <v-tabs-items v-model="tabs">
            <v-tab-item value="CREATE">
              <v-card class="tab-item-container" color="transparent" flat>
              <v-text-field placeholder="Username" class="ma-0 pa-0" type="text" hint="3 or more characters" required> </v-text-field>
              <v-text-field placeholder="Email" class="ma-0 pa-0 my-1" type="email" hint="6 or more characters" required> </v-text-field>
              <v-text-field placeholder="Password" class="ma-0 pa-0" :type="show1 ? 'text' : 'password'" hint="6 or more characters" required :append-icon="show1 ? 'visibility_off' : 'visibility'" @click:append="show1 = !show1"> </v-text-field>
              <v-text-field placeholder="Confirm Password" class="ma-0 pa-0 my-1" :type="show2 ? 'text' : 'password'" hint="6 or more characters" required :append-icon="show2 ? 'visibility_off' : 'visibility'" @click:append="show2 = !show2"> </v-text-field>
              <v-btn color="primary" hover class="create-acc-btn mt-1" >Create Account</v-btn>
              </v-card>
            </v-tab-item>
            <v-tab-item value="LOGIN">
              <v-card class="tab-item-container" color="transparent" flat>
              <v-text-field placeholder="Email" class="ma-0 pa-0" type="email" hint="6 or more characters" required> </v-text-field>
              <v-text-field placeholder="Password" class="ma-0 pa-0 my-2" :type="show2 ? 'text' : 'password'" hint="6 or more characters" required :append-icon="show3 ? 'visibility_off' : 'visibility'" @click:append="show3 = !show3"> </v-text-field>
              <v-btn color="primary" hover>Sign In</v-btn>
              <v-btn color="primary" hover flat>FORGOT PASSWORD?</v-btn>
              </v-card>
            </v-tab-item>
            <v-tab-item value="FORGOT">
              <v-card class="tab-item-container" color="transparent" flat>
              <v-text-field placeholder="Email" class="ma-0 pa-0 mb-2" type="email" hint="6 or more characters" required> </v-text-field>
              <v-btn color="primary" hover>Send confirmation email</v-btn>
              </v-card>
            </v-tab-item>
          </v-tabs-items>
        </v-layout>
      </v-card>
      </v-dialog>
    </v-toolbar>
    <v-navigation-drawer v-model="drawer" fixed clipped id="navigation-drawer" :width="250" temporary>
      <div class="scroll-fix"></div>
      <v-list id="drawer-list" data-simplebar="init">
        <v-divider></v-divider>
        <v-list-tile to="/" ripple active-class="primary--text" active class="pt-2">
          <v-list-tile-action class="pl-2 " >
            <v-icon>home</v-icon>
          </v-list-tile-action>
          <v-list-tile-content class="pl-2">
            Home
          </v-list-tile-content>
        </v-list-tile>
        <v-list-tile to="/trending" ripple>
          <v-list-tile-action class="pl-2">
            <span class="mdi mdi-fire"></span>
          </v-list-tile-action>
          <v-list-tile-content class="pl-2">
            Trending
          </v-list-tile-content>
        </v-list-tile>
        <v-list-tile  to="/categories" ripple>
          <v-list-tile-action class="pl-2" >
            <span class="mdi mdi-apps"></span>
          </v-list-tile-action>
          <v-list-tile-content class="pl-2">
            Categories
          </v-list-tile-content>
        </v-list-tile>
        <v-list-tile  @click="searchFocus()" ripple class="pb-2">
          <v-list-tile-action class="pl-2" >
            <span class="mdi mdi-magnify"></span>
          </v-list-tile-action>
          <v-list-tile-content class="pl-2">
            Search
          </v-list-tile-content>
        </v-list-tile>
        <v-divider></v-divider>
        <v-subheader class="subheading grey--text text--darken-1">ACCOUNT</v-subheader>
        <v-list-tile   @click="changeDiaClassLoginDrawer()" ripple>
          <v-list-tile-action class="pl-2" >
            <span class="mdi mdi-login"></span>
          </v-list-tile-action>
          <v-list-tile-content class="pl-2">
            Sign In
          </v-list-tile-content>
        </v-list-tile>
        <v-list-tile  @click="changeDiaClassCreateDrawer()" ripple class="pb-2">
          <v-list-tile-action class="pl-2" >
            <span class="mdi mdi-account-plus"></span>
          </v-list-tile-action>
          <v-list-tile-content class="pl-2">
            Create Account
          </v-list-tile-content>
        </v-list-tile>

        <v-divider></v-divider>
        <v-subheader class="subheading grey--text text--darken-1">CONTACT</v-subheader>

        <v-list-tile @click="contactDialogChange()" ripple>
          <v-list-tile-action class="pl-2" >
            <span class="mdi mdi-message-alert"></span>
          </v-list-tile-action>
          <v-list-tile-content class="pl-2">
            Contact Us
          </v-list-tile-content>
        </v-list-tile>
        <v-list-tile  href="https://discordapp.com/" target="_blank" ripple>
          <v-list-tile-action class="pl-2" >
            <span class="mdi mdi-discord"></span>
          </v-list-tile-action>
          <v-list-tile-content class="pl-2">
            Discord
          </v-list-tile-content>
        </v-list-tile>
        <v-list-tile  href="https://twitter.com/papes_io" target="_blank" ripple>
          <v-list-tile-action class="pl-2" >
            <span class="mdi mdi-twitter"></span>
          </v-list-tile-action>
          <v-list-tile-content class="pl-2">
            Twitter
          </v-list-tile-content>
        </v-list-tile>
      </v-list>
    </v-navigation-drawer>

    <v-dialog v-model="contactDialog" class="dialog-container" height="675px" width="450px" transition="slide-y-transition">
      <v-card class="dialog-contact">
        <v-card class="dialog-top" color="rgba(0,0,0,0)" flat >
          <v-layout row wrap>
            <v-flex xs1>
              <v-btn icon large  class="title " @click="contactDialog = false"><v-icon>close</v-icon></v-btn>
            </v-flex>
            <v-flex xs10>
              <v-card-text center class="tab-title">
                Contact Us
              </v-card-text>
            </v-flex>
          </v-layout>
          <v-card class="tab-item-container" color="transparent" flat>
          <v-text-field placeholder="Name" class="ma-0 pa-0 pb-1" type="text" required> </v-text-field>
          <v-text-field placeholder="Email" class="ma-0 pa-0 my-1 pb-1" type="email" hint="6 or more characters" required> </v-text-field>
          <v-textarea placeholder="Message" class="ma-0 pa-0 pb-1" hint="500 characters or less" required maxlength="500"> </v-textarea>
          <v-btn color="primary" hover class="create-acc-btn mt-1" >Send</v-btn>
          </v-card>
        </v-card>
      </v-card>
    </v-dialog>
    <v-slide-y-transition mode="out-in">
      <nuxt />
    </v-slide-y-transition>
    <div class="main-footer-container">
      <div class="main-footer-text">
        <v-container grid-list-xs,sm,md,lg,xl>
          <v-layout row wrap>
            <v-flex xs6 sm3 class="pl-5">
              <h4 class="mt-5 mb-3">Directory</h4>
              <a href="#"><p>Home</p></a>
              <a href="#"><p>Browse</p></a>
              <a href="#"><p>Random</p></a>
              <a href="#"><p>Search</p></a>
              <a href="#"><p>Recent</p></a>
            </v-flex>
            <v-flex xs6 sm3 class="pl-5">
              <h4 class="mt-5 mb-3">Business</h4>
              <a href="#"><p>Staff</p></a>
              <a href="#"><p>What's New</p></a>
              <a href="#"><p>Upcoming</p></a>
            </v-flex>
            <v-flex xs6 sm3 class="pl-5">
              <h4 class="mt-5 mb-3">Resources</h4>
              <a href="#"><p>Cookie Policy</p></a>
              <a href="#"><p>Advertising</p></a>
            </v-flex>
            <v-flex xs6 sm3 class="pl-5">
              <h4 class="mt-5 mb-3">Connect</h4>
              <a href="#"><p>Conact Us</p></a>
              <a href="#"><p>Discord</p></a>
              <a href="#"><p>Facebook</p></a>
              <a href="#"><p>Twitter</p></a>
              <a href="#"><p>Youtube</p></a>
            </v-flex>
          </v-layout>
        </v-container>
      </div>
    </div>
    <div class="main-footer-io"><p>papes<span class="glow">.</span>io</p></div>
  </v-app>
</template>

<script>



  export default {
    data () {
      return {
        drawer: false,
        dialog: false,
        toolActive: false,
        tabs: "FORGOT",
        show1: false,
        show2: false,
        show3: false,
        tabText: "",
        scrollPosition: null,
        title: 'Vuetify.js',
        contactDialog: false
      }
    },
    methods: {
      changeDiaClassLogin(){
        this.tabs = "LOGIN"
        this.tabText = "Sign In"
      },
      changeDiaClassCreate(){
        this.tabs = "CREATE"
        this.tabText = "Create Account"
      },
      changeDiaClassCreateDrawer(){
        this.drawer = false
        this.dialog = true
        this.tabs = "CREATE"
        this.tabText = "Create Account"
      },
      changeDiaClassLoginDrawer(){
        this.drawer = false
        this.dialog = true
        this.tabs = "LOGIN"
        this.tabText = "Sign In"
      },
      updateScroll() {
        this.scrollPosition = window.scrollY
      },
      searchFocus(){
        this.drawer = false
        this.$refs.searchBar.focus()
      },
      contactDialogChange(){
        this.drawer = false
        this.contactDialog = true
      }
    },
    mounted() {
     window.addEventListener('scroll', this.updateScroll);
   }
  }
</script>

<style>
body{
background: rgb(23,24,26);
}
.theme--dark.application {
  background: transparent;
}
a:link {
  color: inherit;
  text-decoration: none;
}
a:visited {
  color: inherit;
}
a:hover {
  color: inherit;
}
a:active {
  color: inherit;
}
.glow{
color: #f3c669;
text-shadow: 0 0 1px #f3c669;
}

#toolbar{
z-index: 100;
background-color: rgba(0,0,0,0);
}
#toolbar.toolbar-scroll{
background-color: rgba(15,15,15, 0.99);

}
#navigation-drawer{
background: rgb(52, 52, 52);
}
.v-navigation-drawer__border{
display: none;
}
#drawer-list{
padding-top: 67px;
}
.mdi{
font-size: 24px;
}
.drawer-active{
color: #f3c669;
}
.input-card{
height: 70%;
width: 30vw;
min-width: 200px;
position: absolute;
left: 50%;
margin-left: -15vw;
}
#search-bar{
text-align:center;
}
#search-bar::placeholder{
text-align:left;
color: rgba(255, 255, 255, 0.4);
padding-left: 14px;
}
.input-card .v-text-field>.v-input__control>.v-input__slot:before{
border: 0;
}
.toolbtn{
font-size: 17.5px;
}
.scroll-fix{
position: fixed;
top: 0;
left: 0;
width: 100%;
z-index: 101;
height: 80px;
background: -webkit-linear-gradient(180deg,#303030 0,#303030 60%,rgba(48,48,48,0) 100%);
background: -moz-linear-gradient(180deg,#303030 0,#303030 60%,rgba(48,48,48,0) 100%);
background: -ms-linear-gradient(180deg,#303030 0,#303030 60%,rgba(48,48,48,0) 100%);
background: -o-linear-gradient(180deg,#303030 0,#303030 60%,rgba(48,48,48,0) 100%);
background: linear-gradient(180deg,#303030 0,#303030 60%,rgba(48,48,48,0) 100%);
}
.v-dialog{
overflow: hidden;
margin: 0;
}
.dialog-account{
background: url("../static/dialog-pic.png") top center/cover no-repeat;
width: 450px;
height: 675px;
border: 1px solid rgba(255, 255, 255, 0.6);
}
.dialog-contact{
background: url("../static/contact-pic.png") top center/cover no-repeat;
width: 450px;
height: 675px;
border: 1px solid rgba(255, 255, 255, 0.6);
}
.dialog-contact textarea{
  resize: none;
  height: 225px;
}
.dialog-top{
height: 185px;
width: 100%;
}

.tab-item-container{
text-align: center;
width: 400px;
border-radius: 0;
margin: auto;
padding-top: 30px;
}
.tab-item-container .v-text-field>.v-input__control>.v-input__slot{
padding: 10px 24px;
background: rgba(10,10,10,0.7);
transition: 0.2s;
border-bottom: 1px solid rgba(255, 255, 255, 0);
}
.tab-item-container .v-text-field>.v-input__control>.v-input__slot:hover{
  border-bottom: 1px solid rgba(255, 255, 255, 0.1);
}
.tab-item-container .v-text-field>.v-input__control>.v-input__slot:before{
border: 0;
}
.tab-item-container .v-btn{
width: 100%;
margin: 0;
height: 44px;
margin-bottom: 10px;
}
.tab-item-container .create-acc-btn{
  height: 50px;
}


.tab-title{
font-size: 22px;
text-shadow: 0 0 1px darkgrey;
text-align: center;
}
.main-footer-container{
  background: #0a0a0b;
  width: 100%;
  padding-bottom: 100px;
}
.main-footer-text{

  margin: auto;
  max-width: 1100px;
  font-size: 15px;
}
.main-footer-text p{
  font-weight: 300;
  opacity: 0.7;
  transition: 0.2s;
}
.main-footer-text p:hover{
  opacity: 1;
}
.main-footer-io{
  position: relative;
  bottom: 0;
  text-align: center;
  padding-bottom: 20px;
  padding-top: 30px;
  font-size: 20px;
  width: 100%;
  background: #070708;
}
.v-dialog:not(.v-dialog--fullscreen) {
  max-height: 100%
}
@media only screen and (max-width: 770px) {
.toolbtn{
  padding: 0;
  margin: 0;
}
}
@media only screen and (max-width: 450px) {
.create-acc{
 display: none;
}
}
@media only screen and (max-width: 530px), screen and (max-height: 650px) {
.v-dialog{
  box-shadow: none;
}
.dialog-account, .dialog-contact{
  margin: auto;
  width: 305px;
  height: 420px;
}
.dialog-contact textarea{
  resize: none;
  height: 110px;
}
.dialog-top{
  height: 40px;
  width: 100%;
}
.tab-item-container{
  width: 255px;
  padding-top: 10px;
}
.tab-item-container .v-text-field>.v-input__control>.v-input__slot{
  padding: 2px 24px;
}
.tab-title{
  font-size: 17px;
}
.mdi-key-variant, .mdi-login, .mdi-account-plus{
  font-size: 18px;
}
}
</style>
