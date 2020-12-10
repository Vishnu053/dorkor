<template>
  <div>
    <v-expansion-panels>
      <v-expansion-panel v-for="(item, i) in items" :key="i">
        <v-expansion-panel-header style="font-weight: 700" class="pl-3">
          {{ item.title }}
        </v-expansion-panel-header>
        <v-expansion-panel-content
          v-for="(d, i) in item.dorkList"
          :key="'d' + i"
        >
          <div
            @click="emitSuggestion(d.dork)"
            class="c-pointer border-bottom-primary mb-2"
          >
            {{ d.text }}
          </div>
        </v-expansion-panel-content>
      </v-expansion-panel>
      <template v-if="localItems.dorkList.length > 0">
        <v-expansion-panel>
          <v-expansion-panel-header style="font-weight: 700" class="pl-3">
            {{ localItems.title }}
          </v-expansion-panel-header>
          <v-expansion-panel-content>
            <div
              v-for="(d, i) in localItems.dorkList"
              :key="'d' + i"
              class="row mx-0 mb-2"
            >
              <div
                @click="emitSuggestion(d.dork)"
                class="c-pointer border-bottom-primary col-10 pa-0"
              >
                {{ d.text }}
              </div>
              <div class="col pa-0 t-a-r">
                <v-btn small icon color="error" class="pt-2"
                  ><v-icon class="mdi mdi-close" @click="removeCustomDork(i)"
                /></v-btn>
              </div>
            </div>
            <v-btn
              small
              text
              color="primary"
              class="text-capitalize px-0 float-right mt-3"
              @click="customDorkDialog = !customDorkDialog"
              >Create New Dork</v-btn
            >
          </v-expansion-panel-content>
        </v-expansion-panel>
      </template>
      <div v-else class="mt-2">
        No custom dorks created.
        <v-btn
          small
          text
          color="primary"
          class="text-capitalize px-0"
          @click="customDorkDialog = !customDorkDialog"
          >Create New Dork</v-btn
        >
      </div>
    </v-expansion-panels>
    <!-- create new custom dork dialog-->
    <v-dialog v-model="customDorkDialog" width="500">
      <v-card>
        <v-card-title class="headline primary"> New Dork </v-card-title>

        <v-card-text>
          <v-text-field label="Title" v-model="newDork.text" />
          <v-text-field label="Dork Command" v-model="newDork.dork" />
        </v-card-text>

        <v-divider></v-divider>

        <v-card-actions>
          <v-spacer></v-spacer>
          <v-btn color="error" text @click="customDorkDialog = false">
            Cancel
          </v-btn>
          <v-btn
            :disabled="
              newDork.text.trim().length < 1 || newDork.dork.trim().length < 1
            "
            color="primary"
            text
            @click="createNewCustomDork"
          >
            Create
          </v-btn>
        </v-card-actions>
      </v-card>
    </v-dialog>
    <!-- new dork created -->
    <v-snackbar
      top
      center
      v-model="dorkCreatedSnackBar"
      :timeout="3000"
      color="success"
    >
      <div class="white--text">Custom dork created!</div>
    </v-snackbar>
    <!-- dork removed -->
    <v-snackbar
      top
      center
      v-model="dorkRemovedSnackBar"
      :timeout="3000"
      color="error"
    >
      <div class="white--text">Custom dork removed!</div>
    </v-snackbar>
  </div>
</template>

<script>
import trendJson from "../../public/content/trends.json";
export default {
  data: () => ({
    selectedItem: 1,
    items: trendJson.items,
    localItems: {
      title: "My Custom Dorks",
      icon: "mdi-clock",
      dorkList: [],
    },
    customDorkDialog: false,
    newDork: {
      text: "",
      dork: "",
    },
    dorkCreatedSnackBar: false,
    dorkRemovedSnackBar: false,
  }),
  mounted() {
    this.getUserDefinedDorks();
  },
  methods: {
    emitSuggestion(item) {
      this.$emit("emittedSuggestion", item);
    },
    getUserDefinedDorks() {
      let d = localStorage.getItem("myCustomDorks");
      if (d) {
        console.log(d);
        this.localItems.dorkList = JSON.parse(
          localStorage.getItem("myCustomDorks")
        );
      }
    },
    createNewCustomDork() {
      this.localItems.dorkList.push(this.newDork);
      localStorage.setItem(
        "myCustomDorks",
        JSON.stringify(this.localItems.dorkList)
      );
      this.newDork = { text: "", dork: "" };
      this.customDorkDialog = false;
      this.dorkCreatedSnackBar = true;
    },
    removeCustomDork(i) {
      this.localItems.dorkList.splice(i, 1);
      localStorage.setItem(
        "myCustomDorks",
        JSON.stringify(this.localItems.dorkList)
      );
      this.dorkRemovedSnackBar = true;
    },
  },
};
</script>

<style>
</style>