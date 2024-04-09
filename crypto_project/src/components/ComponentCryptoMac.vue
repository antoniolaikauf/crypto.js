<script>
import CryptoJS from "crypto-js";
export default {
  name: "componentCrypto_mac",
  mounted() {
    let salt = CryptoJS.lib.WordArray.random(128 / 8);
    let key = CryptoJS.PBKDF2("ciao", salt, { keySize: 128 / 32 });
    console.log(key);
    //Encrypt Data
    var encryptObject = CryptoJS.AES.encrypt("ciao", key.toString());

    //Calculate HMAC
    // output del tag
    // nel tag si passa il messaggio e la key
    var tag = CryptoJS.HmacSHA512(encryptObject.toString(), key.toString());
    // invio messaggio
    let transitmessage = tag.toString() + encryptObject.toString();
    console.log(tag);

    // tag
    var transithmac = transitmessage.substring(0, 128);
    console.log(transithmac.toString());
    // testo crittato
    var transitencrypted = transitmessage.substring(128);
    console.log(transitencrypted);
    var decryptedhmac = CryptoJS.HmacSHA512(transitencrypted, key.toString()).toString();
    console.log(decryptedhmac.toString());
    // alert(transithmac == decryptedhmac);
    var decrypted = CryptoJS.AES.decrypt(transitencrypted, key.toString());
    // alert(decrypted.toString(CryptoJS.enc.Utf8));
  },
};
</script>
<template>
  <h3>Sicurezza del messaggio / Integrità del messaggio MAC</h3>
  <p>
    Il MAC viene usato per verificare se il messaggio è stato modificato. È composto da due algoritmi: uno <b>S/FIRMA</b> e uno <b>V/VERIFICA</b>. La
    firma, come input, ha il messaggio e la chiave, e l'output è un tag. Questo tag poi viaggia con il messaggio fino al destinatario e, con
    l'algoritmo V, verifica se il messaggio è stato modificato. Quindi, l'output di questo algoritmo è yes o no, controllando se il messaggio è stato
    modificato con attacchi di integrità, che sono attacchi che modificano il testo. Il procedimento per il controllo è che si produce la chiave e il
    testo cifrato; dopo si crea il <b>TAG</b> (var tag = CryptoJS.HmacSHA512(encryptObject.toString(), key.toString());) inserendo il messaggio e la
    chiave. Una volta fatto questo, si concatena con il testo cifrato, essendo che devono viaggiare insieme, e il tag è "appeso" al messaggio. Una
    volta fatto, si divide la stringa esadecimale ottenuta. In questo caso, quello che ho trovato online non è molto sostenibile, essendo che se si
    cambia la posizione della concatenazione del tag e del testo cifrato non funziona più. Ovviamente, il messaggio con il tag deve essere diviso
    correttamente. In questo caso, si è usato HmacSHA512 per creare il tag; quindi, il tag sarà una stringa di 512 bit che, in esadecimale,
    corrisponde a 128 caratteri (8 bit sarebbero 2 caratteri esadecimali, e il risultato è 128). Quindi, si dividono i primi 128 caratteri che
    corrispondono al tag, e il resto è il testo cifrato: <b>var tag = transitmessage.substring(0, 128);</b>
    <b>var textCrypted = transitmessage.substring(128);</b>. Una volta ottenuto il testo cifrato, si utilizza ancora il metodo per creare un
    HmacSHA512, inserendo il testo cifrato (textCrypted) e la chiave. Se il risultato ottenuto è uguale al tag che abbiamo estratto (la variabile tag)
    dalla stringa, composta dal tag e dal messaggio, allora il messaggio non è stato modificato.
  </p>
</template>
<style></style>
