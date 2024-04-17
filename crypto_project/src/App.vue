<script>
import componentCrypto_cipher from "./components/ComponentCryptoCipher.vue";
import componentCrypto_key from "./components/ComponentCryptoKey.vue";
import componentCrypto_mac from "./components/ComponentCryptoMac.vue";
import desProcedimento from "./components/ComponentCryptoNote.vue";

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
  <div class="container-fluid">
    <div class="row">
      <div class="col-3">
        <div id="list-example" class="list-group"></div>
        <a class="list-group-item list-group-item-action" href="#list-item-1">Item 1</a>
        <a class="list-group-item list-group-item-action" href="#list-item-2">Item 2</a>
        <a class="list-group-item list-group-item-action" href="#list-item-3">Item 3</a>
        <a class="list-group-item list-group-item-action" href="#list-item-4">Item 4</a>
      </div>
      <div class="col-9">
        <div data-bs-spy="scroll" data-bs-target="#list-example" data-bs-offset="0" class="scrollspy-example col-9" tabindex="0">
          <div id="list-item-1"><componentCrypto_key /></div>
          <div id="list-item-2"><componentCrypto_cipher /></div>
          <div id="list-item-3"><componentCrypto_mac /></div>
          <div id="list-item-4"><desProcedimento /></div>
        </div>
      </div>
    </div>
  </div>
</template>

<style lang="scss">
@import "./style/general.scss";
</style>
