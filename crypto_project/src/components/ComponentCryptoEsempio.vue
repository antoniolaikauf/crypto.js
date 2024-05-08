<script>
import CryptoJS from "crypto-js";
export default {
  name: "EsCrypto_js",
  data() {
    return {
      key: "",
      key_hex: "",
      key_crypto_js: "",
    };
  },
  methods: {
    ciphertext() {
      for (const caracter of this.key) {
        this.key_hex += caracter.charCodeAt(0).toString(16);
      }
      this.key_crypto_js = CryptoJS.enc.Hex.parse(this.key_hex);
      console.log(this.key_crypto_js);
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
