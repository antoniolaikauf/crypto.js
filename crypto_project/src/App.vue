<script>
import componentCrypto_cipher from "./components/ComponentCryptoCipher.vue";
import componentCrypto_key from "./components/ComponentCryptoKey.vue";
import componentCrypto_mac from "./components/ComponentCryptoMac.vue";

export default {
  components: {
    componentCrypto_key,
    componentCrypto_cipher,
    componentCrypto_mac,
  },
};
</script>

<template>
  <div style="position: relative">
    lavoro in corso
    <componentCrypto_key />
    <componentCrypto_cipher />
    <componentCrypto_mac />
  </div>
</template>

<style>
* {
  font-family: "Courier New", Courier, monospace;
}
</style>
