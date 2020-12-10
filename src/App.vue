<template>
  <v-app>
    <v-main>
      <router-view />
           <!-- SW update snackbar -->
    <v-snackbar bottom center v-model="updateExists" :timeout="-1" color="primary">
  <div class="row mx-2"><div class="col-8 pb-0 pt-2">Update available!</div>
  <v-btn small class="col-4 py-0 mt-1 primary--text" color="white" @click="refreshApp">
    Update
  </v-btn>
  </div>
</v-snackbar>
    </v-main>

  </v-app>
</template>

<script>
import update from '@/mixins/sWorkerUpdate.js'
export default {
  name: "App",
  mixins: [update],
  data: () => ({
    drawer: false,
    //
  }),
  created() {
    this.$vuetify.theme.dark = true;
  },
};
</script>
<style>
.border-primary {
  border: 0.5px solid var(--v-primary-base);
}
.border-secondary {
  border: 0.5px solid var(--v-secondary-base);
}
.v-text-field__details {
  height: 0;
  display: none;
}
.c-pointer {
  cursor: pointer;
}
.border-top-primary{
  border-top: 1px solid var(--v-primary-base);
}
.border-bottom-primary{
  border-bottom: 1px solid var(--v-primary-base);
}
body{
  scroll-behavior: smooth;
}
.t-a-r{
  text-align: right;
}
</style>
<style>
@import url("https://fonts.googleapis.com/css2?family=Inconsolata:wght@400;500;700;900&display=swap");
.v-application,.app-title {
  font-family: "Inconsolata", monospace !important;
}
.app-title{
  font-size: 3em;
}
</style>