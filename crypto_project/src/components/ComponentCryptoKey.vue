<script>
import CryptoJS from 'crypto-js';
export default {
  name: "componentCrypto_key",
  data() {
    return {
      message: "",
      algoritmo: "",
      key: "",
      algoritmi: ["AES", "DES", "TripleDES", "Rabbit", "RC4", "RC4Drop"],
      message_decropted: "",
      message_encrypted: "",
      hexString: "",
      salt:'',
    };
  },
  methods: {
    // metodo per ora commentato 
    trasform() {
      // ogni words rappresenta 32 bits
      // stringbits  prende i primi 16 bytes dall'array words quindi le prime 4 parole in array words
      // il salt rappresenterebbe la randomicità cosi che la key anche con lo stesso input l'output di key128bits sarà sempre diverso
      // var salt1 = CryptoJS.lib.WordArray.random(128 / 8);
      // var key128Bits = CryptoJS.PBKDF2(this.key, salt1, {
      //   keySize: 128 / 32,
      // });
      // console.log(key128Bits.toString());
      // console.log(key128Bits);
      // // CIPHER COMMENTATO
      // // cipher AES E usa CBC come defaul value
      // this.message_encrypted = CryptoJS.AES.encrypt(this.message, key128Bits.toString());
      // // cipher AES D
      // this.message_decropted = CryptoJS.AES.decrypt(this.message_encrypted, key128Bits.toString());
      // console.log(this.message_encrypted);
      // console.log(this.message_decropted.toString(CryptoJS.enc.Utf8));
      // console.log(this.message_encrypted.toString());
    },
  },
  mounted() {
    // key lunga 192 bits quindi avrà 24 bytes dato da sigbytes
    // word lunga per forza 32 bit 0 64
    // nell'array words ci saranno 6 stringhe di numeri interi questo è dato da 192/32 se ce ne sono di piu è perchè potrebbero venire aggiunte
    // le word sono usate per manipolare i dati di input e produrre output sicuri.
    // il salt usato per radomicità  cosi che anche se input rimane lo stesso l'output sarà sempre diverso
    // this.salt = CryptoJS.lib.WordArray.random(128 / 8);
    // this.hexString = CryptoJS.PBKDF2("ciao", this.salt, { keySize: 128 / 32 });

    // console.log(this.hexString);
    // // Converti l'output in una stringa esadecimale
    // this.hexString = this.hexString.toString(CryptoJS.enc.Hex);
    // this.salt=this.salt.toString(CryptoJS.enc.Hex)
    // console.log(this.salt);
 

  },
};
</script>

<template>
  <section>
    <h1>documentazione di crypto.js</h1>
  <h3>
    spero che questa documentazione sia utile essedno che sto iniziando a imparare della crittografia e ho trovato poco utile la documentazione di
    crypto.js (mette li del codice ma non ti spiega molto bene)
  <div>
    <a href="https://cryptojs.gitbook.io/docs#pbkdf2"> questo è il link per la documentazione</a>
    https://cryptojs.gitbook.io/docs#pbkdf2 <br>
    <a href="https://nodejs.org/api/crypto.html">altro link</a>
     https://nodejs.org/api/crypto.html <br>
     un link dove spiega un po il PBKDF2 <a href="https://github.com/johanns/crypto-js/issues/101">link github</a> https://github.com/johanns/crypto-js/issues/101
  </div>
  </h3>
  <div>
    <h3>generazione della key</h3>
    <p>
      var salt = CryptoJS.lib.WordArray.random(128 / 8); <br> var key128Bits = CryptoJS.PBKDF2("Secret Passphrase", salt, { keySize: 128 / 32 });<br> var
      key256Bits = CryptoJS.PBKDF2("Secret Passphrase", salt, { keySize: 256 / 32 }); <br> var key512Bits = CryptoJS.PBKDF2("Secret Passphrase", salt, {
      keySize: 512 / 32 }); <br> var key512Bits1000Iterations = CryptoJS.PBKDF2("Secret Passphrase", salt, { keySize: 512 / 32, iterations: 1000 }); <br>
      sulla documentazione c'è scritto questo con poco testo che descrie cosa succede. <br>
      <ol>
        <li>
          salt : il salt permette di dare randomicità alla funzione per generare la key, questo perche non vogliamo usare la stessa key per due messaggi inviati. La lunghezza dell salt è di 128 bits 
          in questo caso la stringa salt è {{ salt }} la lunghezza del salt non deve essere necessariamente uguale a quella della key che si vuole usare 
         </li>
        <li>
          ora pr quanto riguarda riguarda la generazione della <b> key</b> prima bisogna passargli la password come input in questo caso scegliamo 'ciao', il secondo parametro è il  <b>salt</b> cosi che anche se la password rimane ciao l'output della key 
          sarà sempre diverso il terzo parametro è la <b> keysize/keylen</b> che gestisce i bit della key generata, la lunghezza di bit del  metodo PBKDF2 deve essere in base all'algroitmo dove la vuoi inserire  es. con AES usi una key lunga 128/192/256 nel DES 64 3DES 168.
          da quello che ho visto online le word all'interno dell'array sono sempre 8 anche se teoricamente dovrebbero essere 4 essendo che 128/32 fa 4 ogni parola all'interno dell'array words è composta da 32 bits  , un altra cosa importante è il <b>sigBytes</b> essendo che ci  dice 
          quanti byte ha la key nel caso che abbiamo fatto è  16 perche 16 * 8 fa 128 bitsche sarebbero la lunghezza della key. Se si mettesse es 128/16 la quantità  delle word nell'array words non cambia rimane 8 ma nel <b>sigBytes</b> cambia a 32 e risulta sbagliato teoricamente 
          essendo che 32 bytes  * 8 fa 256 bits e quindi va oltre la lunghezza della key ( non so se è una cosa di crypto.js e sistema sta cosa o sono io che ho cercato male su internet e sigBytes non si riferisce alla lunghezza della key) , <b>il contenuto all'interno dell'array words sarebbe la key generata</b>
          <b>l'iterazione</b> specifica il numero di volte che la funzione di derivazione della chiave viene eseguita. L'uso di molteplici iterazioni serve a rendere il processo di derivazione della chiave più resistente contro attacchi di forza bruta 
         <br>  questo è il risultato della key con lunghezza 128 bits per usare in un AES {{ hexString }}
        </li>
      </ol>
    </p>
  </div>
  <!-- <form action="" @submit.prevent="trasform">
    <div>
      <input type="text" v-model="message" />
    </div>
    <div>
      <label for="password"> inserisci password</label>
      <input type="password" name="" id="password" v-model="key" />
    </div>
    <select name="" id="" v-model="algoritmo">
      <option value="null" selected>scegli algoritmo</option>
      <option v-for="(algoritmo, i) in algoritmi" :value="algoritmo">{{ algoritmo }}</option>
    </select>
    <input type="submit" value="crea" />
  </form>

  <div>
    {{ message_decropted }}
  </div>
  <div>
    {{ message_encrypted }}
  </div> -->
  </section>
</template>

<style scoped>
.read-the-docs {
  color: #888;
}
</style>
