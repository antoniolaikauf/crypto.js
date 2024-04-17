<script>
import CryptoJS from "crypto-js";
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
      salt: "",
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
    this.salt = CryptoJS.lib.WordArray.random(128 / 8);
    this.hexString = CryptoJS.PBKDF2("ciao", this.salt, {
      keySize: 128 / 32,
      iterations: 1000,
    }).toString(CryptoJS.enc.Hex);
    // Converti l'output in una stringa esadecimale
    this.hexString = this.hexString.toString(CryptoJS.enc.Hex);
    // console.log(this.hexString);
    this.salt = this.salt.toString(CryptoJS.enc.Hex);
    // console.log(this.salt);
  },
};
</script>

<template>
  <section>
    <div>
      <h3>Generazione della key</h3>
      <p>
        var salt = CryptoJS.lib.WordArray.random(128 / 8); <br />
        var key128Bits = CryptoJS.PBKDF2("Secret Passphrase", salt, { keySize: 128 / 32 });<br />
        var key256Bits = CryptoJS.PBKDF2("Secret Passphrase", salt, { keySize: 256 / 32 }); <br />
        var key512Bits = CryptoJS.PBKDF2("Secret Passphrase", salt, { keySize: 512 / 32 }); <br />
        var key512Bits1000Iterations = CryptoJS.PBKDF2("Secret Passphrase", salt, { keySize: 512 / 32, iterations: 1000 }); <br />
        Sulla documentazione c'è scritto questo con poco testo che descrive cosa succede. <br />
        Un link dove spiega un po' il PBKDF2
        <a href="https://github.com/johanns/crypto-js/issues/101">link GitHub</a> https://github.com/johanns/crypto-js/issues/101
        <ol>
          <li>
            salt: il salt permette di dare randomicità alla funzione per generare la key, questo perché non vogliamo usare la stessa key per due messaggi
            inviati. La lunghezza del salt è di 128 bits in questo caso. La lunghezza del salt non deve essere necessariamente uguale a quella della key
            che si vuole usare.
          </li>
          <li>
            Per quanto riguarda la generazione della <b>key</b>, inizialmente è necessario inserire la password come input; in questo caso scegliamo
            'ciao'. Il secondo parametro è il <b>salt</b>, così che, anche se la password rimane 'ciao', l'output della <b>key</b> sarà sempre lierso. Il
            terzo parametro è la <b>keysize/keylen</b>, che gestisce i bit della <b>key</b> generata. La lunghezza in bit del metodo PBKDF2 deve essere
            adeguata all'algoritmo in cui si intende utilizzare la <b>key</b>; ad esempio, con AES si usa una <b>key</b> lunga 128, 192 o 256 bit, nel DES
            64 bit e nel 3DES 168 bit. Da quello che ho visto online, le parole all'interno dell'array sono sempre otto, anche se teoricamente dovrebbero
            essere quattro, essendo che 128/32 fa 4. Ogni parola all'interno dell'array di parole è composta da 32 bit. Un altro elemento importante è il
            <b>sigBytes</b>, che ci dice quanti byte ha la <b>key</b>. Nel caso che abbiamo considerato è 16, perché 16 * 8 fa 128 bit, che sarebbero la
            lunghezza della <b>key</b>. Se si impostasse, ad esempio, 128/16, la quantità delle parole nell'array words non cambia, rimane 8, ma in
            <b>sigBytes</b> cambia a 32, il che teoricamente è sbagliato, essendo che 32 byte * 8 fa 256 bit e quindi va oltre la lunghezza della
            <b>key</b> (non so se è una caratteristica di Crypto.js o se ho cercato male su internet e <b>sigBytes</b> non si riferisce alla lunghezza
            della <b>key</b>). <b>Il contenuto all'interno dell'array words sarebbe la key generata</b>.
    
            <b>L'iterazione</b> specifica il numero di volte che la funzione di derivazione della chiave viene eseguita. L'uso di molteplici iterazioni
            serve a rendere il processo di derivazione della chiave più resistente contro gli attacchi di forza bruta. Questo è il risultato della
            <b>key</b> con lunghezza 128 bit per essere usata in AES. Questo fa riferimento alla crittografia simmetrica, ma per quanto riguarda la
            crittografia asimmetrica, bisognerebbe generare più chiavi. Per quanto riguarda la crittografia asimmetrica, ci possono essere due modi per
            generare le chiavi: uno può essere il PBKDM, dove si usa direttamente la password, e per quanto riguarda l'HDKM, ha due fasi principali
            chiamate espansione ed estrazione, e in entrambe le fasi utilizza un PRF che sarà un HMAC come funzione. Ma in entrambi i casi, sia per PBKDM
            che per HDKM, è necessario produrre una stringa di tot bit in base a quante chiavi vogliamo, e dopo troncare quella stringa in più chiavi.
            Queste due stringhe faranno riferimento alla password <b>key</b> inserita all'interno del PBKDF e HKDF. Nella crittografia simmetrica non è un
            problema, essendo che la chiave si usa sia per decifrare che per cifrare il messaggio (ricordarsi di cambiarla ogni volta, altrimenti si
            rischia di subire degli attacchi, essendo che facendo la xor tra due <b>key</b> uguali il risultato è 0).
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
