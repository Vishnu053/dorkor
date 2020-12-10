<template>
  <v-expansion-panels>
    <v-expansion-panel v-for="(item, i) in items" :key="i">
      <v-expansion-panel-header style="font-weight: 700;" class="pl-3"> {{ item.title }} </v-expansion-panel-header>
      <v-expansion-panel-content v-for="(d,i) in item.dorkList" :key="'d'+i">
        <div @click="emitSuggestion(d.dork)" class="c-pointer border-bottom-primary">{{d.text}}</div>
      </v-expansion-panel-content>
    </v-expansion-panel>
  </v-expansion-panels>
</template>

<script>
import trendJson from '../../public/content/trends.json'
export default {
  data: () => ({
    selectedItem: 1,
    items: trendJson.items,
  }),
  methods: {
    emitSuggestion(item) {
      this.$emit("emittedSuggestion", item);
    },
  },
};
</script>

<style>
</style>