<script>
export default {
  name: "typeCypher",
};
</script>
<template>
  <section>
    <h3>Crittografia</h3>
    <p>
      La crittografia può essere divisa in due categorie: <b>crittografia assimetrica (o anche detta crittografia a chiave pubblica)</b> e
      <b>crittografia simmetrica</b>. Nella crittografia simmetrica, la chiave viene usata sia per decifrare che per cifrare il messaggio, quindi si
      avrà solo una coppia di chiavi: una per il MAC e una per l'encoder. <br />
      Per quanto riguarda la crittografia asimmetrica, la libreria non lo supporta; è adatta solo alla crittografia simmetrica. Se si volesse
      utilizzare la crittografia simmetrica, si dovrebbe usare la libreria
      <a href="https://github.com/digitalbazaar/forge?tab=readme-ov-file#introduction"><b>forge</b></a> (Forge non offre tutte le sue funzionalità,
      non ci sono le architetture dei cifrari a blocchi e lo stesso vale per i MAC, cosa che Crypto.js offre).La crittografia asimmetrica, oltre ad
      utilizzare un algoritmo di cifratura (E) e uno di decifratura (D), utilizza un altro algoritmo <b>(chiamato G)</b> per generare una coppia di
      chiavi, chiamate pubblica (PB) e privata (SK). Come unico input, l'algoritmo G richiede la lunghezza desiderata della chiave.
      <b>L'output di G sarà una coppia di chiavi pubblica e privata</b>. Per iniziare a comunicare, bisognerà inviare la chiave pubblica al
      destinatario. Il mittente utilizzerà la chiave pubblica del destinatario per cifrare il suo messaggio. Una volta che il destinatario avrà
      ricevuto il testo cifrato, utilizzerà la sua chiave privata per decifrare il messaggio e ottenere il testo in chiaro. <br />
      La crittografia asimetrica si basa sulla <b>teoria dei numeri</b> e sul modulo inverso specialmente sui <b>teoremi di Fermat e Eulero</b>. La
      teoria di fermat afferma se p è primo e se a è un intero non divisibile per p, allora vale la congruenza a^p-1 ≡ 1(modp), il che significa che
      se si divide ap−1 per p si ottiene come resto 1. Se invece si volesse ottenere il valore che moltiplicato ad a facesse 1 modp sarebbe a^p-2=
      a^-1
      <a href="https://www.treccani.it/enciclopedia/piccolo-teorema-di-fermat_%28Enciclopedia-della-Matematica%29/"><b>Teorema di fermat</b></a>
      Es. p=7 zp={1,2,3,4,5,6} se si prendesse una x dal'insieme di zp e lo si elevasse a p-1 si otterrebbe sempre 1 modp 3^6=729=1 mod 7, se invece
      si volesse trovare l'inverso si eleverebbe alla p-2 Es. p=7 Zp={1,2,3,4,5,6} a=3 quindi x*a =1 modp ora bisognerebbe trovare x in modo tale che
      che moltiplicato per a faccia 1 modp quindi si prende a e lo si eleva alla p-2 quindi 3*5=243=5 mod p quindi l'inverso di a (a^-1) sarebbe 5 se
      prendiamo l'equazione di prima e sostituiamo x con 5, 5 * 3 = 15 =1 mod p <br />. Per quanto riguarda la teoria di
      <a href="https://www.treccani.it/enciclopedia/teorema-di-eulero-fermat_%28Enciclopedia-della-Matematica%29/"><b>Eulero</b></a> si usa quando p
      non è primo quindi su N e si basa sulla <b>coprimibilità</b> cioè la relazione tra due numeri ad essere coprimi gcd(x,N)=1, quindi N può essere
      anche un numero pari e riguarda la funzione <b>phi ϕ</b> ϕ(N), questo insieme sarebbe composto da tutti i valori coprimi tra 1 a phi-1 ED N Es.
      N=12 ϕ(12)={1,5,7,11}=4 e il teorema afferma che se x appartenente ad Zn (questo insieme {1,5,7,11}) è coprimo con N allora x^ϕ(N)=1 mod N,
      5^4=81=1 mod N. Invece per quanto riguarda calcolare il numero che moltiplicato faccia 1 mod N si eleva ϕ-1 Es. p=12 Zn={1,5,7,11} a=5 quindi
      x*a =1 modp, (a deve appartenere ad Zn) x*5=1 mod N 5^ϕ-1=5^3=125=5mod N quindi x sarà 5 5*5=250 1 mod N. In crittografia asimmetrica, i vari
      algoritmi condividono il concetto di utilizzo di <b>funzioni one-way</b>, che sono facili da calcolare in una direzione ma difficili da
      invertire senza informazioni aggiuntive. Per cifrare un messaggio, si usa la chiave pubblica e il messaggio stesso come input, e si produce un
      messaggio cifrato questo sarebbe l'output della funzione one-way. Questo messaggio cifrato, non può essere decifrato facilmente senza l'uso
      della corrispondente chiave privata, che funge da funzione inversa nel processo di decifratura. <br />
      <b>Durante la pratica non si deve fare direttamente sul testo in chiaro questo procedimento</b>, ma si usa per calcolare poi una key tramite una
      funzione hash e questa key dopo verrà usata per cifrare il messaggio e si avra cosi una crittografia ibrida. I protocolli piu usati sono il
      <b>RSA</b> e il <b>diffie hellman</b> . <br />
      Per quanto riguarda la sicuezza del diffie hellman si basa sulla probabilità che non esiste
      <b>nessun algoritmo efficiente che riesce a calcolare g^ed</b> dato g dato g^e e g^d, un modo per calcolare e avendo d sarebbe calcolare la
      <b>th root</b> di e e quindi calcolare d ma calcolare e è difficile perchè si basa sul problema del logaritmo disceto che si usa con numeri
      interi all'interno di un campo finito. <br />
      Per la sicurezza del RSA si basa <b>sulla fattorizazione di phi(n)</b>, dato la chiave pubblica e l'output della funzione one way, la
      probabilita che un algoritmo efficiente riesca a calcolare la secret-key è trascurabile. Prima spieghiamo le proprietà di e,d che sarebbero due:
      la prima è che devono essere coprimi di <b>phi(n)</b>, phi(n)=(q-1)*(p-1) in cui p e q sono due valori primi e devono essere piu o meno di
      dimensioni uguali e l'altra è che e,d <q>devono essere inversi modulari tra di loro</q> quindi e*d=1 modphi(n), detto questo calcolare d avendo
      e è difficile <q>essendo che d deve essere coprimo con phi(n) e per calcolare phi(n) bisognerebbe fattorizzare n quindi calcolare q e p</q> due
      pagine per capire bene RSA <a href="https://it.wikipedia.org/wiki/RSA_(crittografia)">wiki RSA</a>,
      <a
        href="https://www.telsy.com/le-funzioni-one-way-e-trapdoor-il-cuore-della-crittografia-moderna/#:~:text=Funzioni%20one%2Dway%20nella%20crittografia%20a%20chiave%20pubblica&text=Pi%C3%B9%20formalmente%2C%20sia%20f%20%3A%20A,b%20f(a)%3Db"
      >
        RSa/trapdoor tdf</a
      >
      Per quanto riguarda i procedimenti del crittografia RSA che viene spesso usato nei protocolli tls/ssl prima di usare le funzione rsa si fa il
      procedimento del <b>OAEP Optimal Asymmetric Encryption Padding</b> <br />
      <img src="../../public/img/oaep.png" alt="" class="img_oaep" /> <br />
      per il OAEP ci possono essere piu versioni per esempio il <b>OAEP+</b>
      <a href="https://www.shoup.net/papers/oaep.pdf">(paper scientifico del OAEP+)</a> o il <b>SAEP</b> <br />
      La parte sinistra dell'immagine precedentemente <b>sarebbe il messaggio con bit di zero</b> (la quantità di bit varia in base allo standard
      utilizzato), mentre la parte di destra sarebbe composta <b>da bit randomici</b>.
      <b
        >Nel primo processo, si farebbe la XOR tra la parte di sinistra e la funzione hash con input i bit randomici. La parte successiva sarebbe la
        XOR tra la funzione hash, con input la parte precedentemente elaborata, e i bit randomici. Questi due blocchi verranno poi inseriti nella
        funzione RSA.</b
      >
      La lunghezza di questo output finale è di 2048 bit. <br />Se si volesse decifrare l'output, prima di tutto bisognerebbe utilizzare la funzione
      inversa per riottenere output della funzione precedente <b> la one way function</b> dopo si dovra dividere troncarlo in modo tale da ricavare i
      due blocchi separatamente, una volta fatto si calcolano i bit randomici con la xor tra la hash function con dentro la parte destra dell'output
      diviso e la parte di sinistra, in questo modo si calcolano i bit randomici, una volta fatto questo si decifra la parte di destra con la xor tra
      la parte destra e la hash function dei bit randomici una volta ottenuto questa parte si divide in modo tale che si trova m e tutti i bit di 0
      che si ha messo e se i bit di 0 ottenuti combaciano l'output sarà m se no rifiuta il testo cifrato e l'output sara la ⊥ <br />
      <img src="../../public/img/enc-dec.png" class="oaep_e_d" alt="" /> <br />
    </p>
  </section>
</template>
<style lang="scss" scoped>
@use "./../style/partials/_partials.scss" as *;
section {
  margin: $margin;
  .img_oaep,
  .oaep_e_d {
    width: 50%;
  }
}
</style>
