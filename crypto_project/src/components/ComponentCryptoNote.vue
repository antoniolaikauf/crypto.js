<script>
export default {
  name: "desProcedimento",
};
</script>
<template>
  <section>
    <p>
      In sostanza, per cifrare e decifrare un messaggio, è necessario utilizzare una chiave e un 'salt', che introduce la randomicità essenziale per
      evitare l'uso ripetuto della stessa chiave, circostanza che potrebbe esporre a rischi di attacchi. <br />
      Ecco un esempio di come generare un salt e una chiave di 128 bit utilizzando la libreria CryptoJS: var salt = CryptoJS.lib.WordArray.random(128
      / 8); var key128Bits = CryptoJS.PBKDF2(Secret Passphrase, salt, { keySize: 128 / 32 }); Per la cifratura e la decifratura, si utilizzano due
      funzioni, encrypt e decrypt. Nella cifratura, si passa la chiave e il messaggio da cifrare; nella decifratura, si utilizza il testo cifrato e la
      stessa chiave: var encrypted = CryptoJS.AES.encrypt(Message, key); var decrypted = CryptoJS.AES.decrypt(encrypted, key); Questo è il
      procedimento di base per cifrare e decifrare un messaggio. <br />
      <!-- teoria  -->
      È molto importante sottolineare che, per crittografare del testo, si dovrebbero utilizzare standard come <b>CCM</b>, <b>GCM</b> ed <b>EAX</b>.
      <br />
      Questi standard sono sviluppati dal <b>National Institute of Standards and Technology (NIST)</b> e rappresentano modalità che garantiscono sia
      la confidenzialità sia l'integrità dei dati. Pertanto, sono modelli che resistono sia ad attacchi all'integrità (in cui il messaggio potrebbe
      essere stato modificato) sia a violazioni della confidenzialità, assicurando che solo le parti autorizzate possano accedere al contenuto di un
      dato o messaggio. <br />
      Se un modello crittografico è immune e resistente a attacchi come CCA (Chosen Ciphertext Attack) e CPA (Chosen Plaintext Attack), si può dire
      che fornisce crittografia autentica, poiché combina la confidenzialità garantita dalla cifratura con l'integrità e l'autenticazione offerte dal
      MAC. Tutte queste modalità sono a nonce-based encryption cioè oltre alla key fanno uso di un nonce (il nonce deve cambiare ogni volta che si
      invia un messaggio) e, se ci sono dati invalidi, fermeranno la connessione e si capirà perché l'output sarà una ⊥.
      <br />
      Per quanto riguarda la struttura dei <b>pacchetti</b> (i pacchetti sono delle 'buste' che conterranno un header e un payload), si deve usare una
      <b>IPsec</b> che consiste prima nell'encrypt then MAC e come input del MAC ci sarà il testo cifrato, questo perché facendo così il tag farà
      riferimento al testo cifrato e, se il testo cifrato verrà modificato, si potrà accorgere immediatamente. Per quanto riguarda i <b>modelli</b>,
      il <b> CCM</b> consiste in un CBC-MAC e come cifratura si usa un CTR, il <b>GCM</b> consiste in un GHASH (WC-MAC) e come cifratura un CTR, e il
      <b>EAX</b> consiste in un CMAC e un CTR. Quindi un pacchetta sarà formato da questi due componenti <br />
      Un argomento che riguarda ancora la chiave è che viene divisa in due: una per la <b>cifratura</b> e una per la <b>decifratura</b>, e ognuna di
      queste ha a sua volta una chiave per il <b>MAC</b> e una per i <b>cifrari</b>.
      <b> La chiave per la cifratura e la decifratura sono diverse e questo si chiama crittografia asimmetrica</b>, dove solo la chiave di decifratura
      può decifrare il testo cifrato, poiché è legata alla chiave di cifratura. La forza di un sistema di crittografia asimmetrica si basa sulla
      difficoltà di determinare la chiave privata corrispondente alla chiave pubblica. Invece, per quanto riguarda la crittografia simmetrica, la
      stessa chiave è usata sia per cifrare che per decifrare; la libreria Crypto.js supporta la crittografia simmetrica e per tutti i modelli sopra
      citati utilizzano la crittografia simmetrica. <br />
      Una caratteristica molto importante per i cifrari è la <b>non linearità</b>, che avviene tramite complesse operazioni matematiche:
      <b>una piccola modifica al testo in chiaro o alla chiave porterà a un output completamente diverso</b>, per esempio nell'AES si ha la S-box,
      mentre per la <b>linearità</b> sono coinvolte operazioni matematiche semplici come l'addizione e lo XOR. Nel One-Time Pad (OTP), se non ci fosse
      un PRG che da un seed genera ogni volta una chiave diversa, si potrebbe considerare un cifrario lineare, essendo che per cifrare un messaggio si
      consiste nello XOR tra il messaggio e la chiave.
    </p>
  </section>
</template>
<style lang="scss" scoped>
@use "./../style/partials/_partials.scss" as *;
section {
  margin: $margin;
}
</style>
