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
  <div class="container">
    <div class="row">
      <div style="position: relative">
        lavoro in corso
        <componentCrypto_key />
        <componentCrypto_cipher />
        <componentCrypto_mac />
      </div>
    </div>
  </div>
</template>

<style lang="scss">
@import "./style/general.scss";
</style>
