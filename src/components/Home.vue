<template>

  <v-container>
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
        <!-- <h2 class="headline font-weight-bold mb-3">
          What's next?
        </h2> -->

        <v-row justify="center">
          <v-col cols="12" sm="6">
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
    <!-- <div>Icons made by <a href="https://www.flaticon.com/authors/srip" title="srip">srip</a> from <a href="https://www.flaticon.com/" title="Flaticon">www.flaticon.com</a></div> -->
  </v-container>

</template>

<script>

  export default {
    name: 'HelloWorld',

    data: () => ({
      message:""
    }),
    methods:{
      search(){

      }
    }

  }

</script>
