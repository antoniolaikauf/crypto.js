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
      si volesse trovare l'inverso si eleverebbe alla p-2 Es. p=7 Zp={1,2,3,4,5,6} a=3 quindi x*a =1 modp ora bisognerebbe trovare x in modo tale
      che che moltiplicato per a faccia 1 modp quindi si prende a e lo si eleva alla p-2 quindi 3*5=243=5 mod p quindi l'inverso di a (a^-1) sarebbe 5
      se prendiamo l'equazione di prima e sostituiamo x con 5, 5 * 3 = 15 =1 mod p <br />.
    </p>
  </section>
</template>
<style></style>
