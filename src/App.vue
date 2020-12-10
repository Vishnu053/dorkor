<template>
  <v-app>
    <v-main>
      <router-view />
    </v-main>
  </v-app>
</template>

<script>
export default {
  name: "App",

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