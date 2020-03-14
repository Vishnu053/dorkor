<template>
  <v-container>
    <v-row class="text-center">
      <v-col cols="12">
        <v-img :src="require('../assets/logo.png')" class="my-3" contain height="200" />
      </v-col>

      <v-col class="mb-4">
        <h3 class="display-2 font-weight-bold mb-3">Dorkor</h3>
      </v-col>

      <v-col class="mb-5" cols="12">
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

      <v-col class="mb-5" cols="12">
        <v-icon small class="mb-3">mdi-help</v-icon>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
export default {
    data(){
        return{
            message:""
        }
    },
    methods:{
        search(){
            // https://www.google.com/search?q=site%3Alinkedin.com%2Fin+
            var m=encodeURI(this.message)
            window.open(`https://www.google.com/search?q=${m}`)
        }
    }
};
</script>

<style>
::-webkit-scrollbar{
    width:0px;
    background: #fff0;
}
::-webkit-scrollbar-thumb{
    color: #2196f3;
}
::-webkit-scrollbar-track{
    background: #fff0;
}
</style>