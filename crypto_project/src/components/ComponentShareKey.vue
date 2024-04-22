<script>
export default {
  name: "ShareKey",
};
</script>
<template>
  <section>
    <p>
      Per ottenere la key condivisa nella documentazione non c'è scritto niente essendo ma si può fare in due modi. <br />
      Il primo modo è quello di affidarsi a una 3 persona/protocollo <b>TTP</b> che fornira una key condivisa generata da loro, questo procedimento
      funziona che le due persone che vogliono ottenere la key condivisa hanno la propria key e la forniscono alla terza persona, questa prima
      genererà una random key e una volta generata la si invia tramite testo codificato. <br />
      Al primo utente che ha richiesto la key al protocollo si invia un testo codificato e l'output di questo è dato dall'input della key che questa
      persona ha inviato al protocollo e il messaggio, il messaggio sarebbe una concatenazione tra una frase esempio "key alice e bobo" e la key che è
      stata generata dal protocollo cosi che se decodifica il testo cifrato usando la sua key potra ottenere la key generata dal protocollo, invece
      per quanto riguarda l'altra persona riceverà un ticket che consiste in un testo cifrato come quello precedentemente soltato che al posto della
      key dell'altra persona sarà la sua cosi che potra decifrare il testo cifrato e otterrà la key del protocollo, in questo modo tutte e due le
      persone condividono una key. <br />
      Una cosa molto importante è che per ottenere questa key il protocollo eve essere online e un altro aspetto è che se un aggressore riesce a
      superare la sicurezza di questo protocollo potrebbe ottenere le key condivise quindi ci sono anche dei svantaggi
    </p>
  </section>
</template>
<style></style>
