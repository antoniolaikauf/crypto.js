<script>
import componentCrypto_cipher from "./components/ComponentCryptoCipher.vue";
import componentCrypto_key from "./components/ComponentCryptoKey.vue";
import componentCrypto_mac from "./components/ComponentCryptoMac.vue";
import desProcedimento from "./components/ComponentDesProcesso.vue";

export default {
  components: {
    componentCrypto_key,
    componentCrypto_cipher,
    componentCrypto_mac,
    desProcedimento,
  },
};
</script>

<template>
  <div class="container">
    <div class="row">
      <div style="position: relative">
        <componentCrypto_key />
        <componentCrypto_cipher />
        <componentCrypto_mac />
        <desProcedimento />
      </div>
    </div>
  </div>
</template>

<style lang="scss">
@import "./style/general.scss";
</style>
