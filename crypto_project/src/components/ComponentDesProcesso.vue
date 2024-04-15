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
  <!-- teoria  -->
  <p>
    È molto importante sottolineare che, per crittografare del testo, si dovrebbero utilizzare degli standard come CCM, GCM ed EAX. Questi standard
    sono sviluppati dal National Institute of Standards and Technology (NIST) e rappresentano delle modalità che garantiscono sia la confidenzialità
    sia l'integrità dei dati. Pertanto, sono modelli che resistono sia ad attacchi all'integrità (in cui il messaggio potrebbe essere stato
    modificato) sia a violazioni della confidenzialità, assicurando che solo le parti autorizzate possano accedere al contenuto di un dato o messaggio
    quindi soggetti ad attacchi CCA (Chosen Ciphertext Attack) e CPA (Chosen Plaintext Attack).
  </p>
</template>
<style></style>
