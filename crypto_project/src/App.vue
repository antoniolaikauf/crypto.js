<script>
import componentCrypto_cipher from "./components/ComponentCryptoCipher.vue";
import componentCrypto_key from "./components/ComponentCryptoKey.vue";

export default {
  components: {
    componentCrypto_key,
    componentCrypto_cipher,
  },
};
</script>

<template>
  <div style="position: relative">
    lavoro in corso
    <componentCrypto_key />
    <componentCrypto_cipher />
  </div>
</template>

<style>
* {
  font-family: "Courier New", Courier, monospace;
}
</style>
