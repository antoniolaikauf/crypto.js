<script>
export default {
  name: "desProcedimento",
};
</script>
<template>
  <p>
    In sostanza, per cifrare e decifrare un messaggio, è necessario utilizzare una chiave e un 'salt', che introduce la randomicità essenziale per
    evitare l'uso ripetuto della stessa chiave, circostanza che potrebbe esporre a rischi di attacchi. Ecco un esempio di come generare un salt e una
    chiave di 128 bit utilizzando la libreria CryptoJS: var salt = CryptoJS.lib.WordArray.random(128 / 8); var key128Bits = CryptoJS.PBKDF2(Secret
    Passphrase, salt, { keySize: 128 / 32 }); Per la cifratura e la decifratura, si utilizzano due funzioni, encrypt e decrypt. Nella cifratura, si
    passa la chiave e il messaggio da cifrare; nella decifratura, si utilizza il testo cifrato e la stessa chiave: var encrypted =
    CryptoJS.AES.encrypt(Message, key); var decrypted = CryptoJS.AES.decrypt(encrypted, key); Questo è il procedimento di base per cifrare e decifrare
    un messaggio.
  </p>
</template>
<style></style>
