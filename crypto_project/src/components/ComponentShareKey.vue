<script>
export default {
  name: "ShareKey",
};
</script>
<template>
  <section>
    <p>
      Per ottenere la chiave condivisa, la documentazione non specifica nulla, ma esistono due metodi. Il primo metodo consiste nell'affidarsi a una
      terza persona o a un protocollo TTP (Trusted Third Party), che fornirà una <b>random_key</b> generata da loro. <br />
      Questo processo funziona nel modo seguente: le due persone che desiderano ottenere la chiave condivisa forniscono le proprie chiavi alla terza
      persona, la quale genererà una chiave casuale e, una volta generata, la invierà tramite un testo codificato. Al primo utente che ha richiesto la
      chiave al protocollo si invia un testo codificato, e l'output di questo testo è dato dall'input della chiave che questa persona ha inviato al
      protocollo e dal messaggio, che sarebbe una concatenazione tra una frase esempio "chiave Alice e Bob" e la chiave che è stata generata dal
      protocollo. Così facendo, se decodifica il testo cifrato usando la sua chiave, potrà ottenere la chiave generata dal protocollo. Per quanto
      riguarda l'altra persona, riceverà un ticket che consiste in un testo cifrato simile a quello precedentemente descritto, ma al posto della
      chiave dell'altra persona sarà presente la sua, così che potrà decifrare il testo cifrato e otterrà la chiave del protocollo. In questo modo,
      solo le due persone possono decifrare il messaggio che hanno ottenuto, essendo che solo loro hanno le chiavi che hanno fornito al protocollo
      all'inizio. <br />
      Con questo procedimento, entrambe le persone condividono una chiave. Un aspetto molto importante è che per ottenere questa chiave il protocollo
      deve essere online e, un altro aspetto è che, se un aggressore riesce a superare la sicurezza di questo protocollo, potrebbe ottenere le chiavi
      condivise, quindi ci sono anche dei svantaggi. Questo metodo riguarda la crittografia simmetrica. <br />
      L'altro metodo non utilizza un TTP (Trusted Third Party) e funziona tramite i protocolli <b>Merkle Puzzle</b> e
      <b>Diffie-Hellman</b>
      (DH), che non spiegherò dato che per la libreria non sono molto rilevanti. <br />
    </p>
  </section>
</template>
<style></style>
