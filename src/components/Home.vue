<template>

  <div>
    <v-row
      class="mb-6"
      no-gutters
    >
      <v-col cols="12" sm="12" md="5" lg="5" style="border-right:1px solid #2196f3;">
        <v-row class="text-center">
          <v-col cols="12">
            <v-img :src="require('../assets/logo.png')"
                   class="my-3"
                   contain
                   height="200" />
          </v-col>

          <v-col class="mb-4">
            <h3 class="display-2 font-weight-bold mb-3">
              Dorkor
            </h3>
          </v-col>

          <v-col class="mb-5"
                 cols="12">
            <v-row justify="center">
              <v-col cols="12" sm="11">
              <v-text-field
                  v-model="message"
                  label="What Are You Looking For?"
                  outlined
                  clearable
                  @keydown.enter="search"
                ></v-text-field>
              </v-col>
            </v-row>
          </v-col>

          <v-col class="mb-5"
                 cols="12">
            <v-icon small class=" mb-3">
              mdi-help
            </v-icon>

          </v-col>

        </v-row>
      </v-col>
      <v-col sm="12" md="7" lg="7">
        <v-card
          class="pa-2"
          outlined
          tile
          style="height:600px;"
        >
          <iframe src="https://www.google.com/webhp?igu=1" style="width:100%;height:100%"/>
        </v-card>
      </v-col>
    </v-row>


    <!-- <div>Icons made by <a href="https://www.flaticon.com/authors/srip" title="srip">srip</a> from <a href="https://www.flaticon.com/" title="Flaticon">www.flaticon.com</a></div> -->
  </div>

</template>

<script>

  export default {
    name: 'HelloWorld',

    data: () => ({
      message:""
    }),
    methods:{
      search(){
        // display results in an iframe
        //logic used in searchbar
         var ot = 0,
 nt = 0,
 qmoff = 0,
 qmon = 0,
 invrt = 0,
 hue = 0,
 revert = 0,
 dashboard=0
 for (var i of th) {
 if (i == "new" || i == "theme") {
 nt++;
 }
 if (i == "old" || i == "theme") {
 ot++;
 }
 if (i == "quick" || i == "menu") {
 qmoff++;
 qmon++;
 }
 if (i == "disable" || i == "off" || i == "hide") {
 qmoff++;
 }
 if (i == "enable" || i == "on" || i == "show") {
 qmon++;
 }
 if (i == "invert" || i == "dark" || i == "night" || i == "black") {
 invrt++;
 }
 if (i == "hue") {
 hue++;
 }
 if (i == "revert" || i == "normal" || i == "reset") {
 revert++;
 }
 if (i=="dashboard") {
 dashboard++
 }
 if (i=="assistant" || i=="butler" || i=="dpassistant" || i=="dp assistant") {
   this.searchString = ""
   this.assistantSLideOutShow=true
 }
 }
 // handle menuList
 if (qmon > qmoff) {
 localStorage.setItem("quickMenu", 1);
 this.getSearchParamList();
 this.searchString = "";
 }
 if (qmoff > qmon) {
 localStorage.setItem("quickMenu", 0);
 this.searchParamList = [];
 this.searchString = "";
 }
 // end handle menuList
 // theming
 if (nt >= 2) {
 localStorage.setItem(btoa("theme"), btoa("new"));
 this.searchString = "";
 this.loadThemeSettings();
 }
 if (ot >= 2) {
 localStorage.setItem(btoa("theme"), btoa("old"));
 this.searchString = "";
 this.loadThemeSettings();
 }
 if (invrt >= 1) {
 localStorage.setItem(btoa("invert"), btoa(1));
 this.loadThemeSettings();
 this.searchString = "";
 }
 if (hue >= 1) {
 localStorage.setItem(btoa("hue"), btoa(1));
 $('body').css("filter","hue-rotate(45deg)")
 document.getElementsByClassName(
 "navbar-static-side"
 )[0].style.background = "#001c3cba";
 this.searchString = "";
 }
 if (revert >= 1) {
 localStorage.setItem(btoa("invert"), btoa(0));
 localStorage.setItem(btoa("hue"), btoa(0));
 this.loadThemeSettings();
 this.searchString = "";
 }
 //end logic  
        
        
        
        
      }
    }

  }

</script>
