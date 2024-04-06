<script>
import CryptoJS from "crypto-js"
export default {
  name: "componentCrypto",
  mounted() {
    const encryptedText = CryptoJS.AES.encrypt("Hi There!", "Secret Passphrase").toString();
    console.log(encryptedText);

    var encrypted = CryptoJS.AES.encrypt("Message", "Secret Passphrase");

    var decrypted = CryptoJS.AES.decrypt(encrypted, "Secret Passphrase");

    console.log(encrypted);
    console.log(decrypted);
  },
};
</script>

<template></template>

<style scoped>
.read-the-docs {
  color: #888;
}
</style>
