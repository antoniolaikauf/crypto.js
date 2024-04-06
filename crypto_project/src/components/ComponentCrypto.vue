<script>
import CryptoJS from "crypto-js";
export default {
  name: "componentCrypto",
  data() {
    return {
      message: "",
      algoritmo: "",
      key: "",
      algoritmi: ["AES", "DES", "TripleDES", "Rabbit", "RC4", "RC4Drop"],
    };
  },
  methods: {
    trasform() {
      //   ogni words rappresenta 32 bits
      // stringbits  prende i primi 16 bytes dall'array words quindi le prime 4 parole in array words
      //   il salt rappresenterebbe la randomicità cosi che la key anche con lo stesso input l'output di key128bits sarà sempre diverso
      var salt = CryptoJS.lib.WordArray.random(128 / 8);
      var key128Bits = CryptoJS.PBKDF2(this.key, salt, {
        keySize: 128 / 32,
      });
      //   convertita la key in esadecimale di 128 bits essendo che deciso sopra quindi le prime 4 words crypto.js aggiunge gia il padding
      var keyHex = key128Bits.toString(CryptoJS.enc.Hex);

      console.log(key128Bits);
      //   cipher AES  E key 128 bits messaggio stesso
      var encrypted = CryptoJS.AES.encrypt(this.message, keyHex);
      //   cypher AES D
      var decrypted = CryptoJS.AES.decrypt(encrypted, keyHex);

      console.log(encrypted);
      console.log(decrypted);
      //  prende una stringa e la trasforma in stringa binaria e to string lo ritrasforma in testo
      console.log(decrypted.toString(CryptoJS.enc.Hex));
    },
  },
  mounted() {},
};
</script>

<template>
  <form action="" @submit.prevent="trasform">
    <div>
      <input type="text" v-model="message" />
    </div>
    <div>
      <label for="password"> inserisci password</label>
      <input type="password" name="" id="password" v-model="key" />
    </div>
    <select name="" id="" v-model="algoritmo">
      <option value="null" selected>scegli algoritmo</option>
      <option v-for="(algoritmo, i) in algoritmi" :value="algoritmo">{{ algoritmo }}</option>
    </select>
    <input type="submit" value="crea" />
  </form>
  lavoro in corso 
</template>

<style scoped>
.read-the-docs {
  color: #888;
}
</style>
