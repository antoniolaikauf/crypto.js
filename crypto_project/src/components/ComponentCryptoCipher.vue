<script>
import CryptoJS from "crypto-js";
export default {
  name: "componentCrypto_cipher",
  data() {
    return {
      algoritmi: [" AES ", " DES ", " TripleDES ", " Rabbit ", " RC4 ", " RC4Drop "],
      salt: "",
      hexString: "",
    };
  },
  mounted() {
    this.salt = CryptoJS.lib.WordArray.random(128 / 8);
    this.hexString = CryptoJS.PBKDF2("ciao", this.salt, { keySize: 128 / 32 }).toString();
    this.hexString2 = CryptoJS.PBKDF2("ciao", this.salt, { keySize: 128 / 32 }).toString();
    // console.log(this.hexString);

    // var encrypted = CryptoJS.AES.encrypt("Message", this.hexString.toString());
    var encrypted = CryptoJS.AES.encrypt("Message", this.hexString);
    var decrypted = CryptoJS.AES.decrypt(encrypted, this.hexString);
    console.log(encrypted);
    console.log(decrypted.toString(CryptoJS.enc.Utf8));

    // const iv = { words: [0, 0, 0, 0], sigBytes: 16 };
    // let code = CryptoJS.AES.encrypt("message", CryptoJS.enc.Utf8.parse("your secret key"), { iv });
    // console.log(code);
  },
};
</script>
<template>
  <section>
    <h3>Algoritmi di crittografia</h3>
    <p>
      I cifrari sono composti da vari elementi. Ci sono i due algoritmi <b>E</b> e <b>D</b> che permettono di cifrare e decifrare i messaggi inviati.
      Questi prendono vari input e restituiscono degli output, come se fossero funzioni. Per quanto riguarda l'algoritmo <b>E</b>, prende la key e il
      messaggio per il <b>D</b>, prende <b>E</b> (che sarebbe il <b>C/testo cifrato</b>) e prende la stessa key per poi decodificare il messaggio che
      è stato inviato dal nostro utente. Questo è il funzionamento base di come funziona un cipher. I cifrari che Crypto.js supporta sono
      <span v-for="(algoritmo, i) in algoritmi">{{ algoritmo }}</span
      >. Per quanto riguarda i cifrari, possono essere di flusso/steam o a blocchi/block. Se vediamo un esempio nella AES, la lunghezza del messaggio
      è di 128 bit. <br />
      var encrypted = CryptoJS.AES.encrypt("Message", "Secret Passphrase"); <br />
      var decrypted = CryptoJS.AES.decrypt(encrypted, "Secret Passphrase"); <br />
      <a href="https://github.com/mpetersen/aes-example/blob/master/README.md">Link per AES</a>.
      <!-- PS: inoltre, qui spiega anche la parte della key  divisa.-->
    </p>

    <ol>
      <li>
        <b>Messaggio</b> consiste nel testo che si vuole cifrare e nell'esempio sopra sarebbe "Message". Qui, la lunghezza del messaggio è di 128 bit
        (16 byte). Se il messaggio è più lungo di 128, viene diviso: prima processerà i 128 bit e poi farà il resto. Se il messaggio è troppo corto,
        gli viene aggiunto il padding fino a che non raggiunge 128 bit. Quindi, nell'oggetto il blocksize si farebbe 'riferimento' alla disponibilità
        del blocco dove viene inserito il messaggio e la lunghezza è di 4. Questo perché in Crypto.js le words vengono fatte in 32 bit (4 byte),
        quindi 128 bit.
      </li>
      <li>
        <b>KEY</b> deve essere di lunghezza adatta al cipher, es. un AES accetta key lunghe 128/192/256 bit, un DES 64. Se si guarda nell'esempio
        sopra, va messa al posto di "Secret Passphrase". Ovviamente, deve essere uguale sia per l'<b>encrypt</b> che per il <b>decrypt</b>.
        Nell'oggetto dell'encrypt, si vede la lunghezza della key con keysize, che specifica 8, quindi sarebbe 8*32=256, ma sarebbe sbagliato; ritorna
        8 essendo che nell'array words ci sono 8 parole anziché 4, come dovrebbe essere. Quindi, se ce ne sono 8, qui ritorna lunghezza della key di
        256 (non sono riuscito a trovare niente riguardante questo, probabilmente è una cosa di Crypto.js già impostata così). Se si vuole vedere, si
        trova nella key array words, in questo caso la sua lunghezza è di sigBytes 32 byte (stessa cosa, non so se è impostata ad avere sempre 8
        parole e poi le seleziona in base alla lunghezza della key data da noi).
      </li>
      <li>
        <b>Testo cifrato</b> si trova nel ciphertext e dentro all'array words conterrà il testo cifrato. Ogni stringa dentro a questo array è di 32
        bits e sigBytes sarebbe la lunghezza di quel testo cifrato. Qui, ovviamente, deve coincidere con i bits del blocksize, quindi 128 bits, 16*8
        fa 128, quindi è corretto.
      </li>
      <li>
        <b>IV</b> questo parametro viene usato solo se si usano modelli specifici, per esempio il CBC (cipher block chain) che utilizza un IV o un
        CTR, tutti e due disponibili in Crypto.js. Non so se si può implementare l'IV con il nonce tramite un metodo della libreria; tuttavia, l'IV
        deve essere della stessa lunghezza del messaggio, quindi del blocksize. Volendo, si può cambiare l'IV.
        <a href="https://github.com/brix/crypto-js/issues/309">Link dove si cambia l'IV</a>.
        <b>Inoltre, ho notato che con questo metodo non si aggiunge il salt nel cipher</b>.
      </li>
      <li>
        <b>Padding</b> viene aggiunto per coprire se il messaggio è troppo corto rispetto ai bit del blocco. Se non si specifica, viene aggiunto
        automaticamente il padding. Non consiste nell'aggiungere tutti 0 fino a riempire il blocco ma ci sono degli standard. Questi sono i padding
        disponibili nella libreria: Pkcs7 (default), Iso97971, AnsiX923, Iso10126, ZeroPadding, NoPadding.
      </li>
      <li>
        <b>Salt</b> sarebbe altra randomicità aggiunta alla key in modo tale che anche se si usa la stessa key non ritorna lo stesso output. PS: (non
        ho ancora capito perché viene aggiunto qui, forse per precauzione che nella creazione della key non venga aggiunto).
      </li>
    </ol>
    <p>
      <b>NOTA BENE</b> <br />
      All'interno di key dentro al cipher si vede che la key viene aumentata. Questo perché nei cifrari di blocco come l'AES la key viene espansa in
      modo tale che ad ogni round si usi una key diversa (probabilmente quel salt viene usato per queste key). Quindi si deduce che ci siano 12 round
      della function round, essendo che ogni word ha 32 bit e ne sono 12, quindi si deduce che la lunghezza è di 384 bits. <br />

      <img src="../../public/img/key_img.png" class="img_key" /> <br />
      Inoltre, questo esempio descrive un AES ma differenti cifrari hanno differenti lunghezze di bit e caratteristiche. Inoltre, tutte le word
      all'interno degli array words sono di 32 bit forzati.
      <a href="https://www.rapidtables.com/convert/number/decimal-to-binary.html">Se si vuole provare</a>.
    </p>
  </section>
</template>

<style scoped>
.img_key {
  width: 50%;
}

@media all and (max-width: 700px) {
  .img_key {
    width: 100%;
  }
}
</style>
