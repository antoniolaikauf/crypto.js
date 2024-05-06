<script>
import componentCrypto_cipher from "./components/ComponentCryptoCipher.vue";
import componentCrypto_key from "./components/ComponentCryptoKey.vue";
import componentCrypto_mac from "./components/ComponentCryptoMac.vue";
import desProcedimento from "./components/ComponentCryptoNote.vue";
import typeCypher from "./components/ComponentCrypto.vue";

export default {
  components: {
    componentCrypto_key,
    componentCrypto_cipher,
    componentCrypto_mac,
    desProcedimento,
    typeCypher,
  },
};
</script>

<template>
  <div class="container-fluid">
    <div class="row">
      <div class="col-12 col-md-2">
        <div id="list-example" class="list-group">
          <a class="list-group-item list-group-item-action" href="#list-item-1">Chiavi</a>
          <a class="list-group-item list-group-item-action" href="#list-item-2">Cifrari</a>
          <a class="list-group-item list-group-item-action" href="#list-item-3">MAC</a>
          <a class="list-group-item list-group-item-action" href="#list-item-5">Type</a>
          <a class="list-group-item list-group-item-action" href="#list-item-4">Note</a>
        </div>
      </div>
      <div class="col-12 col-md-10 mt-5">
        <div data-bs-spy="scroll" data-bs-target="#list-example" data-bs-offset="0" class="scrollspy-example col-9" tabindex="0">
          <h1>Documentazione di Crypto.js e concetti di crittografia</h1>
          <h3>
            Spero che questa documentazione sia utile, essendo che sto iniziando a imparare la crittografia e ho trovato poco utile la documentazione
            di crypto.js.
            <div>
              <ul>
                <li>Il comando per installare è questo: npm install crypto-js e deve essere lanciato nel terminale.</li>
                <li>
                  <a href="https://cryptojs.gitbook.io/docs#pbkdf2">Questo è il link per la documentazione</a>
                  https://cryptojs.gitbook.io/docs#pbkdf2
                </li>
                <li>
                  <a href="https://nodejs.org/api/crypto.html">Altro link</a>
                  https://nodejs.org/api/crypto.html
                </li>
              </ul>
            </div>
          </h3>
          <div id="list-item-5"><typeCypher /></div>
          <div id="list-item-1"><componentCrypto_key /></div>
          <div id="list-item-2"><componentCrypto_cipher /></div>
          <div id="list-item-3"><componentCrypto_mac /></div>
          <div id="list-item-4"><desProcedimento /></div>
        </div>
      </div>
      <div>
        <a href="#" class="back-top"><i class="fa-solid fa-arrow-up"></i></a>
      </div>
    </div>
  </div>
</template>

<style lang="scss">
@import "./style/general.scss";

.back-top {
  position: fixed;
  bottom: 10%;
  border: 1px solid black;
  padding: 8px 10px;
  border-radius: 5px;
  i {
    color: black;
  }
}

#list-example {
  position: fixed;
  top: 0px;
  left: 10px;
}

@media all and (max-width: 760px) {
  #list-example {
    position: fixed;
    left: 0px;
    width: 100%;
    display: flex;
    flex-direction: row;
    border-radius: 0px;
  }
  .back-top {
    right: 20px;
  }
}
</style>
