<script>
import CryptoJS from "crypto-js";
export default {
  name: "EsCrypto_js",
  data() {
    return {
      // variabili per cifratura

      key: "", // key
      keyCyper: "",
      message: "", // messaggio utente
      textCipher: "", // testo cifrato
      tag: "",

      pacchetto: "",
      // variabili per decifratura
      tagDecryption: "", //tag
      textDescryption: "",
      controlloTag: "",
      textDecription: "", // testo decifrato
      messageDecrypt: "",

      comparsa: false, // variabile per comparsa testo
    };
  },
  methods: {
    ciphertext() {
      this.comparsa = true;
      // se non si inserisce l'iv lo metterà di default la libreria
      // var iv = CryptoJS.enc.Hex.parse("101112131415161718191a1b1c1d1e1f"); IV FISSO COSA SBAGLIATA PERCHè IV DEVE ESSERE RANDOMICO E OGNI VOLTA CHE SI CIFRA UN MESSAGGIO NON DEVE ESSERE MAI STATO USATO QUEL IV
      let saltEncyption = CryptoJS.lib.WordArray.random(128 / 32); //generazione sale per dare randomicità
      this.keyCyper = CryptoJS.PBKDF2(this.key, saltEncyption, {
        // generazione key di lunghezza 128 bits si usa un PBKDF e non un HKDF
        keySize: 128 / 32,
      }).toString();

      this.textCipher = CryptoJS.AES.encrypt(this.message, this.keyCyper, {
        // cifratura a blocchi usando un AES
        // archittettura CTR contatore randomizzato
        mode: CryptoJS.mode.CTR,
      }).toString();
      // procedura mac la key deve essere diversa da quella dell'encyption
      let saltMac = CryptoJS.lib.WordArray.random(128 / 32);
      let keyMac = CryptoJS.PBKDF2("frase", saltMac, {
        keySize: 128 / 32,
      }).toString();
      this.tag = CryptoJS.HmacMD5(this.textCipher, keyMac).toString();
      // concatenazione
      this.pacchetto = this.tag + this.textCipher;
      // divisione pacchetto
      this.tagDecryption = this.pacchetto.substring(0, 32);
      this.textDescryption = this.pacchetto.substring(32);

      this.controlloTag = CryptoJS.HmacMD5(this.textDescryption, keyMac).toString();
      // controllo tag se corretto
      if (this.controlloTag === this.tagDecryption)
        alert(`il tag ottenuto ${this.tagDecryption} ed è uguale a ${this.controlloTag} quindi è corretto`);
      else alert(`il tag ottenuto ${this.tagDecryption} ed non è uguale a ${this.controlloTag} quindi è sbagliato `);
      // un avolta ottenuto il tag ed aver controllato si decifra il messaggio
      this.textDecription = CryptoJS.AES.decrypt(this.textDescryption, this.keyCyper, {
        mode: CryptoJS.mode.CTR,
      });

      this.messageDecrypt = this.textDecription.toString(CryptoJS.enc.Utf8);
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
    <div v-if="comparsa">
      <div>Il testo cifrato è il seguente usando un cifrario a blocchi CTR {{ textCipher }}</div>
      <div>Il tag è il seguente usando il HMAC {{ tag }}</div>
      <div>Il pacchetto che riceverà il destinatario sara {{ pacchetto }}</div>
      <div>il messaggio che hai decifrato è: {{ messageDecrypt }}</div>
    </div>
  </section>
</template>
<style scoped lang="scss">
@use "./../style/partials/_partials.scss" as *;

section {
  margin: $margin;
}
</style>
