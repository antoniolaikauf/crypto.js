<script>
import CryptoJS from "crypto-js";
export default {
  name: "componentCrypto_mac",
  mounted() {
    var hash = CryptoJS.SHA256("Message");
    console.log(hash);
    let salt = CryptoJS.lib.WordArray.random(128 / 8);
    let key = CryptoJS.PBKDF2("ciao", salt, { keySize: 128 / 32 });
    // console.log(key);
    //Encrypt Data
    var encryptObject = CryptoJS.AES.encrypt("ciao", key.toString());

    //Calculate HMAC
    // output del tag
    // nel tag si passa il messaggio e la key
    var tag = CryptoJS.HmacSHA512(encryptObject.toString(), key.toString());
    var tag1 = CryptoJS.HmacSHA256(encryptObject.toString(), key.toString());
    // console.log(tag1);
    // invio messaggio
    let transitmessage = tag.toString() + encryptObject.toString();
    // console.log(tag);

    // tag
    var transithmac = transitmessage.substring(0, 128);
    console.log(transithmac);
    // testo crittato
    var transitencrypted = transitmessage.substring(128);
    console.log(transitencrypted);
    var decryptedhmac = CryptoJS.HmacSHA512(transitencrypted, key.toString()).toString();
    // console.log(decryptedhmac.toString());
    // alert(transithmac == decryptedhmac);
    var decrypted = CryptoJS.AES.decrypt(transitencrypted, key.toString());
    // console.log(decrypted.toString(CryptoJS.enc.Hex));
    // alert(decrypted.toString(CryptoJS.enc.Utf8));
  },
};
</script>
<template>
  <section>
    <h3>Sicurezza del messaggio / Integrità del messaggio MAC</h3>
    <p>
      Il MAC(message authenticatio code) viene usato per verificare se il messaggio è stato modificato. È composto da due algoritmi: uno
      <b>S chiamato FIRMA</b> e uno <b>V chiamato VERIFICA</b>. La firma come input ha il messaggio e la chiave, e l'output è un tag. Questo tag poi
      viaggia con il messaggio fino al destinatario e con l'algoritmo V, verifica se il messaggio è stato modificato. Quindi l'output di questo
      algoritmo è yes o no, questo procedimento permette di verificare se il messaggio è stato sggetto da attacchi di integrità, che sarebbero
      attacchi che modificano il testo. Il procedimento è il seguente: Si calcola il tag var hash_i = CryptoJS.SHA256("Message"); questo tag viene
      cocatenato con il messaggio cifrato, una volta che il destinatario riceve la stringa concatenata dovrà sapere come è strutturato il pacchetto
      per poter correttamente separare il tag HMAC dal resto del messaggio. Questo di solito è definito nel protocollo di comunicazione. Una volta
      separata la stringa ricevuta in due parti (il tag e il testo cifrato) si utilizzando la stessa tipologia di algoritmo per generare il tag usato
      dall'utente che ha inviato la stringa concatenata, prendendo il testo cifrato separato dalla stringa ricevuta e usandolo per generare un nuovo
      tag var hash_j = CryptoJS.SHA256(testo cifrato ); se questo hash_j è uguale al tag che abbiamo separato dalla stringa ricevuta dalla persona
      significa che il messaggio non è stato modificato( essendo che con lo stesso messaggio non si può generare tag diversi) una volta confermato si
      procede con l'algoritmo di decodifica per leggere il messaggio. Ovviamente, il messaggio con il tag deve essere diviso correttamente. In questo
      caso, si è usato HmacSHA256 per creare il tag; quindi, il tag sarà una stringa di 256 bit che, in esadecimale, corrisponde a 64 caratteri (8 bit
      sarebbero 2 caratteri esadecimali). Quindi, si dividono i primi 64 caratteri che corrispondono al tag, e il resto è il testo cifrato:
      <b>var tag = transitmessage.substring(0, 64);</b> <b>var textCrypted = transitmessage.substring(64);</b>. La lunghezza del tag dipende da che
      algoritmo si usa. il MAC piu usato è il HMAC ma esistono anche il CBCMAC e la sua variante EMAC(CBCMAC) dove avra due chiavi , stesso vale per
      il NMAC(nested mac) e il PMAC (parallel mac) per quanto riguarda il HMAC essendo che è l'unico supportato da questa libreria ha delle varianti
      (HmacMD5, HmacSHA1, HmacSHA256, HmacSHA512). <br />
      <img src="../../public/img/sha.png" alt="" style="width: 100%" />
      <img src="../../public/img/HMAC.png" alt="" /> <br />
      La formula per HMAC <a href="https://en.wikipedia.org/wiki/HMAC">la puoi trovare qua</a> i due blocchi che all'interno della formula vengono
      concatenati dipendono da che algoritmo si usa se si usa il sha256 sono di 512 bit e per il sha512 sono 1024 bit che dopo vengono compressi a
      ritornare 256 e 512 bit Il opad sarebbe una composizione di byte di 0x5c invece per il ipad sarebbe una composizione di byte di 0x36 per quanto
      riguarda la key o il messaggio se non riescono ad arrivare a 512 bit gli si vinene aggiunto del padding. Nella parte prima dove è presente  XOR tra
      la key e il opad il rsultato sarà di 512 bit se si usa lo sha256, invece nella seconda parte sarà l'output dell'algoritmo H (quindi lo sha256) con all'interno XOR di K e
      ipad concatenato al messaggio, l'output sarà di 256 bit essendo che i bit vengono compressi. Alla fine sarà una concatenazione tra 526 bit della prima
      parte e 256 bit della seconda parte che dopo a sua volta saranno compressi anche loro in 256 bit di output che si riferiranno all'HASH <br />
      L'algoritmo SHA256 è un algoritmo che come input riceve solo il messaggio e come output ritorna un hash che fara riferimento al messaggiinserito
      come input es.
      <b>var hash = CryptoJS.SHA256("Message");</b> ritornerà una stringa lunga 256 bit. Alcune regole per quanto riguarda l'hash è che
      <b>ogni messagio deve avere il proprio hash</b> e non può avere due hash diversi ES H(m1) produrra un solo e unico tag1 che arà riferimento a
      quel messaggio, un altra regola è che <b>non ci può essere un hash per due messaggi uguali</b> se no si rischia di avere un attacco di
      <b>falsificazione essenziale (non sarebbe resistente alla resistance collision)</b> che consiste che da due input diversi si ottiene un output
      uguale ES. H = algoritmo SHA256 H(m0)=H(m1) tale che m0 è diverso da m1 questo algoritmo non è resistente alle collisioni essendo che ha
      prodotto du etag uguali ma con m diversi. Esiste un attacco che si chiama
      <b>
        birthday attack dove si basa sul principio del paradosso del compleanno
        <a href="https://it.wikipedia.org/wiki/Paradosso_del_compleanno"> link per il paradosso del compleanno</a></b
      >
      e sostiene che ci vorrebbero almento 2**1/n dove n sarebbero la lunghezza di una stringa di bit che restituisce il sha256 quindi sarebbero 128
      bit. <br />
      <img src="../../public/img/mac.png" alt="">
    </p>
  </section>
</template>
<style></style>
