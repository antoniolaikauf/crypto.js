<script>
import CryptoJS from "crypto-js";
export default {
  name: "EsCrypto_js",
  data() {
    return {
      key: "",
      key_hex: "",
    };
  },
  methods: {
    ciphertext() {
      for (const caracter of this.key) {
        this.key_hex += caracter.charCodeAt(0).toString(16);
      }
    },
  },
  mounted() {},
};
</script>
<template>
  <section>
    ESEMPIO.
    <div>Inserisci una key <input type="text" v-model="key" /></div>

    <button @click="ciphertext">coonverti</button>
  </section>
</template>
<style scoped lang="scss">
@use "./../style/partials/_partials.scss" as *;

section {
  margin: $margin;
}
</style>
