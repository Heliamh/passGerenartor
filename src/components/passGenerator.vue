<template>
<v-app>
  <v-container class="wrapper">
    <v-row>
     <v-col>
       <p class="whiteText header">Password Generator</p>
     </v-col>
    </v-row>
    <v-row>
     <v-col> <div class="childItem">
       <p class="whiteText">{{showText}}</p>
     </div>

     </v-col>
    </v-row>
    <v-row class="textLeftPosition">
     <v-col>
       <span class="itemTitle">LENGTH: </span> <span class="whiteText">{{ passLength }}</span>
     </v-col>
    </v-row>
    <v-row class="childItem">
      <v-col cols="1" class="pa-1">
        4
      </v-col>
     <v-col class="pa-0">
       <v-slider
           hide-details
           v-model="sliderData.val"
           :track-color="sliderData.color"
           thumb-color="white"
       ></v-slider>
     </v-col>
      <v-col cols="1" class="pa-1">
        32
      </v-col>
    </v-row>
    <v-row class="textLeftPosition">
      <v-col>
        <span class="itemTitle">SETTINGS</span>
      </v-col>
    </v-row>
    <v-row class="childItem">
      <v-col class="pa-0 ">
        Include Uppercase

      </v-col>
      <v-col class="pa-0">
        <v-switch inset v-model="settings.upperCase"/>
      </v-col>
    </v-row>
    <v-row class="childItem">
      <v-col class="pa-0 ">
        Include Lowercase

      </v-col>
      <v-col class="pa-0">
        <v-switch inset  v-model="settings.lowerCase"/>
      </v-col>
    </v-row>
    <v-row class="childItem">
      <v-col class="pa-0 ">
        Include Numbers

      </v-col>
      <v-col class="pa-0">
        <v-switch inset  v-model="settings.numbers"/>
      </v-col>
    </v-row>
    <v-row class="childItem">
      <v-col class="pa-0 ">
        Include Symbols

      </v-col>
      <v-col class="pa-0">
        <v-switch inset  v-model="settings.symbols"/>
      </v-col>
    </v-row>
    <v-row>
     <v-col>
       <v-btn height="45" color="#7986CB" class="generateBtn white--text" @click="generatePassword">
         GENERATE PASSWORD
       </v-btn>

     </v-col>
    </v-row>
  </v-container>
</v-app>
</template>

<script>
export default {
  name: "passGenerator",
  data() {
    return {
      sliderData: {  label: 'track-color', val: 75, color: 'white'},
      showText:'CLICK GENERATE',
      settings:{
        upperCase:true,
        lowerCase:true,
        numbers:true,
        symbols:false
      }
    }
  },
  computed:{
    passLength(){
      return (this.sliderData.val/100*28 + 4).toFixed(0)
    }
  },
  methods:{
    generatePassword() {
      var length = this.passLength,
          charset = "",
          retVal = "";

      if (this.settings.upperCase){
        charset = charset+'ABCDEFGHIJKLMNOPQRSTUVWXYZ'
      }
      if (this.settings.lowerCase){
        charset = charset+'abcdefghijklmnopqrstuvwxyz'
      }
      if (this.settings.numbers){
        charset = charset+'0123456789'
      }
      if (this.settings.symbols){
        charset = charset+'+_)(*&^%$#@!'
      }


      for (var i = 0, n = charset.length; i < length; ++i) {
        retVal += charset.charAt(Math.floor(Math.random() * n));
      }
      this.showText = retVal
    }
  }



}
</script>

<style scoped>
.wrapper {
  background-color: #151d29;
  width: 40%;
  margin: auto;
  padding-inline: 5%;
}

.header {
  margin: 0;
  text-align: left;
  padding-block: 20px;
  font-size: 30px;
}

.whiteText {
  color: white;
}

.childItem {
  color: white;
  text-align: center;
  background-color: #455469;
  margin-inline: auto;
  height: 50px;
  border-radius: 8px;
  margin-block: 10px;
  padding-block: 10px;
}

.textLeftPosition {
  text-align: left;
}

.itemTitle {
  color: #595856;
  font-size: 12px
}


.v-input--selection-controls {
  margin-top: 0px;
  padding-top: 4px;
}

.generateBtn{
  width: 100%;
  border-radius: 8px;
}

</style>
<style>
.v-input__slot {
  place-content: flex-end;
}

</style>