<script>
import CryptoJS from "crypto-js";
export default {
  name: "EsCrypto_js",
  data() {
    return {
      key: "",
      key_hex: "",
      key_crypto_js: "",
      message: "",
      text_cipher: "",
    };
  },
  methods: {
    ciphertext() {
      for (const caracter of this.key) {
        this.key_hex += caracter.charCodeAt(0).toString(16); // si trasforma il testo in esadecimale
      }
      this.key_crypto_js = CryptoJS.enc.Hex.parse(this.key_hex); // si adatta la key esadecimale in modo tale che la libreria mossa usarlo
      this.text_cipher = CryptoJS.AES.encrypt(this.message, this.key_crypto_js.toString(), {
        // si cifra il testo
        mode: CryptoJS.mode.CTR,
      });
      console.log(this.text_cipher);
    },
  },
  mounted() {},
};
</script>
<template>
  <section>
    ESEMPIO.
    <div>Inserisci una key <input type="text" v-model="key" /></div>
    <div>Inserisci il messaggio <input type="text" v-model="message" /></div>

    <button @click="ciphertext">coonverti</button>

    <div>il testo cifrato è il seguente usando un cifrario a blocchi CTR{{ text_cipher.toString(16) }}</div>
  </section>
</template>
<style scoped lang="scss">
@use "./../style/partials/_partials.scss" as *;

section {
  margin: $margin;
}
</style>
