<script>
import CryptoJS from "crypto-js";
export default {
  name: "componentCrypto_cipher",
  data() {
    return {
      algoritmi: [" AES ", " DES ", " TripleDES ", " Rabbit ", " RC4 ", " RC4Drop "],
      salt: "",
      hexString: "",
      selected: false,
    };
  },
  methods: {
    selected_img() {
      if (this.selected) {
        this.selected = false;
      } else {
        this.selected = true;
      }
    },
  },
  mounted() {
    this.salt = CryptoJS.lib.WordArray.random(128 / 8);
    this.hexString = CryptoJS.PBKDF2("ciao", this.salt, { keySize: 128 / 32 });
    // console.log(this.hexString);

    // var encrypted = CryptoJS.AES.encrypt("Message", this.hexString.toString());
    var encrypted = CryptoJS.AES.encrypt("Message", this.hexString.toString(), {
      mode: CryptoJS.mode.CFB,
      padding: CryptoJS.pad.AnsiX923,
    });
    // var decrypted = CryptoJS.AES.decrypt(encrypted, this.hexString);
    // console.log(encrypted);
    // console.log(decrypted.toString(CryptoJS.enc.Utf8));

    // const iv = { words: [0, 0, 0, 0], sigBytes: 16 };
    // let code = CryptoJS.AES.encrypt("message", CryptoJS.enc.Utf8.parse("your secret key"), { iv });
    // console.log(code);
  },
};
</script>
<template>
  <section>
    <h3>algoritmi di crittazione</h3>
    <p>
      i cifrari sono composti da vari elementi ci sono i due algoritmi <b>E</b> e <b>D</b> che permettono di cifrare e decifrare i messaggi inviati
      dopo prendono vari input e restituiscono degli output come se fossero funzioni per quanto riguarda l'algoritmo E prende la key e il messaggio e
      per il D prende E ( che sarebbe la <b>C/testo cifrato </b>) e prend ela stessa key per poi decodificare il messaggio che ha inviato il nostro
      utente . Questo è il funzionamento base di come funzione un cipher , i cifrari che crypto.js supprota sono
      <span v-for="(algoritmo, i) in algoritmi">{{ algoritmo }}</span>
      per quanto riguarda i cifrari possono essere di flusso/steam o a blocchi/block se vediamo un esempio nella AES la lunghezza dell messaggio è di
      128 bit <br />
      var encrypted = CryptoJS.AES.encrypt("Message", "Secret Passphrase"); <br />
      var decrypted = CryptoJS.AES.decrypt(encrypted, "Secret Passphrase"); <br />
      <a href="https://github.com/mpetersen/aes-example/blob/master/README.md">link per AES</a> PS inoltre qua spiega anche la parte della key divisa
      <ol>
        <li>
            <b> messaggio</b> consiste nel testo che si vuole cifrare e nel es sopra sarebbe il Message qua la lunghezza del messaggio è di 128
            bit 16 byte se il messaggio è piu lungo di 128 viene diviso prima processerà i 128 bit e dopo farà il resto , se il messaggio è troppo corto gli viene aggiunto il
            padding fino a che non raggiunge 128 bit, quindi nell'oggetto il blocksize si farebbe 'riferimento' alla disponibilita
            del blocco dove viene inserito il messaggio e la lunghezza è di 4 questo perche in crypto.js le words vengo fatte in 32 bit 4byte quindi 128
            bits
        </li>
        <li>
            <b>KEY</b> deve essere di lunghezza adatta al cipher es un AES accetta key lunghe 128/192/256 bit un DES 64 e se si
            guarda nell'esempio sopra va messa al posto di "Secret Passphrase" ovviamente deve essere uguale sia per il <b>encrypt e decrypt</b> nel oggetto
            dell'encrypt si vede la lunghezza della key con keysize, li specifica 8 quindi sarebbe 8*32 256 , ma sarebbe sbagliato ritorna 8 essendo che
            nell'array words ci sono 8 parola anzichè 4 come dovrebbe essere quindi se ce ne sono 8 qua ritornerà lunghezza della key 8 quindi 256 ( non so
            come mai non sono riuscito a trovare niente riguardante questo probabilmente è una cosa di crypto.js gia inpostata cosi) . se si volesse vedera
            si trova nella key array words in questo caso la sua lunghezza è di sigBytes 32 byte ( stesso cosa non so se è impostata ad avere sempre 8
            parole e dopo le seleziona in base alla lunghezza della key che abbiamo dato noi )
        </li>
        <li>
            <b>testo cifrato</b> si trova nell ciphertext e dentro all'array words conterra il testo cifrato ogni stringa dentro a
            questo array è di 32 bits e sigBytes sarebbe la lunghezza di quel testo cifrato qua ovviamente deve compaciare con i bits del blocksize quindi
            128 bits , 16*8 a 128 quindi è corretto
        </li>
        <li>
            <b>iv</b> questo parametro viene usato solo se si usa modelli specifici per esempio se si usa il CBC cipher block chain che utilizza un iv o un
            CTR tutte e due disponibili in Crypto.js non so se si può implementare l'iv con il nonce tramite un metodo della libreria tuttavia l'ive deve
            essere di stessa l'unghezza del messaggio quindi del blocksize olendo si può cambiare l'iv
            <a href="https://github.com/brix/crypto-js/issues/309"> link dove si cambia l'iv </a>
            <b>inoltre ho notato che con questo metodo non si aggiunge il salt nel cipher</b>
        </li>
        <li>
            <b>padding</b> il padding viene aggiunta per coprire se il messaggio è troppo corto rispetto ai bit del blocco, e se non si specifica viene aggiunto automaticamente 
            il padding non consiste nel aggiungere tutti 0 fino a riempire il blocco ma ci sono delle standard , questi sono i padding che ci sono nella libreria  Pkcs7 (the default)
             Iso97971 AnsiX923 Iso10126 ZeroPadding NoPadding
        </li>
        <li>
            <b>salt</b> sarebbe altra randomicità aggiunta alla key in modo tale che anche se si usa la stessa la stessa key non ritornerà los stesso output
            PS( non ho ancora capito perche viene aggiunto qua forse per precauzione che nella creazione della key non venga aggiunto)
        </li>
     </ol> 
     <p>
        <b>NOTA BENE </b> <br> all'interno di key dentro al cipher si vede che la key venga aumentata questo perche nei cifrari di blocco come l'AES la key
        viene espansa im modo tale che ad ogni round si usi una key diversa ( probabilmente quel salt viene usato per queste key) quindi compare che è
        lunga 384 bits essendo che ogni word ha 32 bit e ne sono 12 quindi da questo si deduce che ci siano 12 round della function round <br>

        <img src="../../public/img/key_img.png" alt="" @click="selected_img" :class="selected ? 'img_big' : 'img_key'" /> <br>
        inoltre questo esempio descrive un AES ma differenti cipher hanno differenti lunghezze di bit e caratteristiche, 
        inoltre tutte le word all'interno degli array words sono di 32 bit forzati <a href="https://www.rapidtables.com/convert/number/decimal-to-binary.html"> se si vole provare</a>
    </p>
    </p>
  </section>
</template>

<style scoped>
.img_key {
  width: 100px;
  
}
.img_big {
  position: absolute;
  width: 50%;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  border: 1px solid black;
}
</style>
