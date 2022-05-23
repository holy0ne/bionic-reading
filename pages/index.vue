<template>
  <v-container fill-height class="align-content-start py-12">
    <v-row class="text-center justify-center">
      <v-col cols="12" class="mb-6">
        <h1>
          <strong>Sim</strong>ple <strong>Bio</strong>nic
          <strong>Read</strong>ing <strong>Conve</strong>rter
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
      "abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZçáéíóúâêîôûãõàèìòùÁÉÍÓÚÂÊÎÔÛÃÕÀÈÌÒÙ",
    numbers: "0123456789",
    currencies: "Ӿ$₴£؋ƒ₼¥₡₱€Q₹₩₭₮₦₫",
    japanese:
      "ーぁあぃいぅうぇえぉおかがきぎくぐけげこごさざしじすずせぜそぞただちぢっつづてでとどなにぬねのはばぱひびぴふぶぷへべぺほぼぽまみむめもゃやゅゆょよらりるれろゎわゐゑをんァアィイゥウェエォオカガキギクグケゲコゴサザシジスズセゼソゾタダチヂッツヅテデトドナニヌネノハバパヒビピフブプヘベペホボポマミムメモャヤュユョヨラリルレロヮワヰヱヲンヴヵヶ゛゜",
    specials: "'",
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
      let current = "";
      let counter = 0;
      let aloc = [];
      aloc[counter] = "";
      const allow = [
        ...this.alphabet,
        ...this.numbers,
        ...this.currencies,
        ...this.japanese,
        ...this.specials,
      ];
      const letters = [...word];
      letters.forEach((w) => {
        const inc = allow.includes(w);
        if (inc) {
          if (current === "puncts") {
            counter++;
            aloc[counter] = "";
          }
          current = "expression";
        } else {
          if (current === "expression") {
            counter++;
            aloc[counter] = "";
          }
          current = "puncts";
        }
        aloc[counter] += w;
      });

      let result = "";
      aloc.forEach((part) => {
        const fl = [...part]?.[0];
        if (allow.includes(fl)) {
          const length = part.length;
          const half = Math.ceil(length / 2);
          const is3 = length === 3;
          const first = part.substring(0, half - (is3 ? 1 : 0));
          const second = part.substring(half - (is3 ? 1 : 0));
          result += "<strong>" + first + "</strong>" + second;
        } else {
          result += part;
        }
      });
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
  border-radius: 8px;
  height: 100%;
  min-height: 130px;
  background-color: lighten($medium, 35);
}
</style>
