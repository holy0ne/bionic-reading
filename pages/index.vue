<template>
  <v-container fill-height class="align-content-start py-12">
    <v-row class="text-center justify-center">
      <v-col cols="12" class="mb-6">
        <h1>
          <strong>Sim</strong>ple <strong>Bio</strong>nic
          <strong>Read</strong>ing <strong>Conve</strong>rsor
        </h1>
      </v-col>
      <v-col class="col-12 col-sm-6">
        <v-textarea
          v-model="text"
          placeholder="Start typing or paste your text..."
          outlined
          auto-grow
          hide-details
        ></v-textarea>
      </v-col>
      <v-col class="col-12 col-sm-6">
        <div class="result" v-html="result" outlined></div>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
export default {
  asyncData({ redirect }) {},
  data: () => ({
    text: "",
    alphabet:
      "abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZáéíóúâêîôûãõàèìòùÁÉÍÓÚÂÊÎÔÛÃÕÀÈÌÒÙ",
    tags: ["<br>"],
  }),
  computed: {
    format() {
      const linebreak = new RegExp("\n", "g");
      return this.text.replace(linebreak, " <br> ");
    },
    result() {
      let final = "";
      const expression = this.format.split(" ");
      expression.forEach((exp) => {
        const isTag = this.tags.includes(exp);
        final += isTag ? exp : exp.replace(exp, this.convert(exp)) + " ";
      });
      return final;
    },
  },
  mounted() {},

  methods: {
    convert(word) {
      if (!word) return "";
      let expression = "";
      let puncts = "";
      const allow = [...this.alphabet, ...["'"]];
      const letters = [...word];
      letters.forEach((w) => {
        const inc = allow.includes(w);
        if (inc) expression += w;
        else puncts += w;
      });
      const length = expression.length;
      const half = Math.ceil(length / 2);
      const is3 = length === 3;
      const first = expression.substring(0, half - (is3 ? 1 : 0));
      const second = expression.substring(half - (is3 ? 1 : 0));
      const result = "<strong>" + first + "</strong>" + second + puncts;
      return result;
    },
  },
};
</script>

<style lang="scss">
@import "~/assets/variables.scss";

h1 {
  font-weight: normal;
}

.result {
  border: 1px solid $medium;
  text-align: left;
  padding: 12px;
  border-radius: 4px;
  height: 100%;
  min-height: 130px;
  background-color: lighten($medium, 35);
}
</style>
