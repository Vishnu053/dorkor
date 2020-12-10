<template>
  <v-container>
    <v-row class="text-center">
      <v-col cols="12">
        <v-img
          :src="require('../assets/logo.png')"
          class="my-3"
          contain
          height="200"
        />
      </v-col>

      <v-col class="mb-0">
        <h3 class="app-title font-weight-bold mb-3">Dorkor</h3>
      </v-col>

      <v-col class="mb-0 py-0" cols="12">
        <v-row justify="space-around">
          <v-col cols="12" sm="11">
            <!-- <v-sheet elevation="10"> -->
            <v-chip-group show-arrows>
              <v-chip
                v-for="tag in tags"
                :key="tag"
                @click="replacewithtag(tag)"
              >
                {{ tag }}
              </v-chip>
            </v-chip-group>
            <!-- </v-sheet> -->
          </v-col>
        </v-row>
        <v-row justify="center">
          <v-col cols="12" sm="11">
            <v-text-field
              ref="searchbox"
              v-model="message"
              label="What Are You Looking For?"
              outlined
              clearable
              @keyup="
                message = message.toLowerCase();
                intelligence();
              "
              @keydown.enter="search"
            ></v-text-field>
          </v-col>
        </v-row>
      </v-col>

      <!-- <v-col class="mb-5" cols="12">
        <v-btn icon fab text small @click="showHelp">
          <v-icon small style="margin-top:7px;" class="mb-3">mdi-help</v-icon>
        </v-btn>
      </v-col> -->
    </v-row>
    <!-- <v-dialog
        v-model="helpDialog"
         :overlay="true"
         style="min-width:500px;min-height:500px;"
        transition="slide-y-reverse-transition"
    >
        <iframe src="./public/content/GoogleCheatSheet.pdf" frameborder="0" height="500px"></iframe>
    </v-dialog>-->
    <v-row class="px-lg-9 px-md-9">
      <v-col cols="12" class="primary--text">Suggestions</v-col>
      <v-col>
        <trends @emittedSuggestion="emittedSuggestion"/>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
import trends from "./trends";
export default {
  components: { trends },
  data() {
    return {
      helpDialog: false,
      message: "",
      tags: [],
      suggestions2: [
        "site:",
        "inTitle:",
        "inUrl:",
        "info:",
        "numrange:",
        "date:",
        "safesearch:",
        "link:",
        "related:",
        "allintitle:",
        "allinurl:",
        "filetype:",
        "ext:",
        "cache:",
        "phonebook:",
        "rphonebook:",
        "bphonebook:",
        "author:",
        "insubject:",
        "define:",
        "stock:",
        "+",
        "-",
      ],
      suggestions: [
        {
          replaceWith: "site:",
          list: ["site", "website"],
        },
        {
          replaceWith: "inTitle:",
          list: ["title", "heading"],
        },
        {
          replaceWith: "inUrl:",
          list: ["title", "heading"],
        },
      ],
      testList: [
        " site ",
        " website ",
        " dated ",
        " everything ",
        " intitle ",
        " inurl ",
      ],
      replaceDork: {
        " site ": " site:",
        " website ": " site:",
        " intitle ": " intitle:",
        " inurl ": " inurl:",
        " url ": " inurl:",
        " address ": " inurl:",
      },
      grammar: [" a ", " an ", " the ", " in ", " on ", " every "],
      sentence: "",
    };
  },
  mounted() {
    this.tags = this.suggestions2;
  },
  methods: {
    async removeGrammar(sentence) {
      this.sentence = sentence;
      var self = this;
      for (let i of self.grammar) {
        this.sentence = this.sentence.replace(i, " ");
      }
      setTimeout(() => {
        return "Done", 500;
      });
    },
    async removetestList(sentence) {
      this.sentence = sentence;
      var self = this;
      for (let i of self.testList) {
        if (self.sentence.includes(i)) {
          self.sentence = self.sentence.replace(i, self.replaceDork[i]);
          console.log(self.sentence);
        }
        //  this.sentence= this.sentence.replace(i," ")
      }
      setTimeout(() => {
        return "Done", 500;
      });
    },
    search() {
      this.removeGrammar(this.message + " ").then((res) => {
        if (this.sentence && this.sentence.length > 0) {
          var m = encodeURI(this.sentence);
          window.open(`https://www.google.com/search?q=${m}`);
        }
      });
    },
    showHelp() {
      // this.removetestList(this.message);
      window.open(
        "https://www.sans.org/security-resources/GoogleCheatSheet.pdf"
      );
    },
    intelligence() {
      var a = this.message.split(" ");
      var b = a[a.length - 1];
      this.tags = [];
      for (let i of this.suggestions2) {
        // console.log(i)
        if (i.toLowerCase().includes(b.toLowerCase())) {
          this.tags.push(i);

          // console.log(i)-+
        }
      }
    },
    replacewithtag(t) {
      var a = this.message.split(" ");
      a[a.length - 1] = t;
      this.message = a.join(" ");
      setTimeout(() => {
        this.$refs.searchbox.focus();
      }, 200);
    },
    emittedSuggestion(i){
     this.message=i
     setTimeout(() => {
        this.$refs.searchbox.focus();
        window.scrollTo({ top: 0, behavior: 'smooth' });
      }, 200);
    }
  },
};
</script>

<style>
::-webkit-scrollbar {
  width: 0px;
  background: #fff0;
}
::-webkit-scrollbar-thumb {
  color: #2196f3;
}
::-webkit-scrollbar-track {
  background: #fff0;
}
</style>