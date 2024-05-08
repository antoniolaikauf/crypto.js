<script>
import CryptoJS from "crypto-js";
export default {
  name: "EsCrypto_js",
  data() {
    return {
      key: "",
      key_hex: "",

      message: "",
      text_cipher: "",
    };
  },
  methods: {
    ciphertext() {

      let salt = CryptoJS.lib.WordArray.random(128 / 8); //generazione sale per dare randomicità 
      this.key_hex = CryptoJS.PBKDF2(this.key, salt, { // generazione key di lunghezza 128 bits si usa un PBKDF e non un HKDF 
        keySize: 128 / 8,
      }).toString();

      this.text_cipher = CryptoJS.AES.encrypt(this.message, this.key_hex, { // cifratura a blocchi usando un AES
        // archittettura CTR contatore randomizzato
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

    <div>il testo cifrato è il seguente usando un cifrario a blocchi CTR {{ text_cipher }}</div>
  </section>
</template>
<style scoped lang="scss">
@use "./../style/partials/_partials.scss" as *;

section {
  margin: $margin;
}
</style>
