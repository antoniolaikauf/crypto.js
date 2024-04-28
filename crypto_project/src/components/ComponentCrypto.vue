<script>
export default {
  name: "typeCypher",
};
</script>
<template>
  <section>
    <h3>Crittografia</h3>
    <p>
        La crittografia può essere divisa in due categorie <b>crittografia assimetrica (o anche detta crittografia a chiave pubblica)</b> e <b>crittografia simmetrica</b>
        nella crittografia simmetrica la key viene usata sia per decifrare che per cifrare il messaggio 
    </p>
  </section>
  Per quanto riguarda la crittografia a chiave pubblica (asimmetrica), essa utilizza un altro algoritmo, chiamato G, che genera una coppia di chiavi
  denominate <b>chiave pubblica e chiave segreta</b>. Se ci sono due persone, Alice e Bob, Alice genererà le due coppie di chiavi e invierà la chiave
  pubblica a Bob. Quest'ultimo sceglierà un testo in chiaro, indicato come x, e utilizzerà la chiave pubblica ricevuta per cifrare il testo e inviarlo
  ad Alice. Quest'ultima userà la chiave segreta che possiede per decifrare il messaggio. <br />
  Un svantaggio di questo metodo è che Bob, se vuole inviare un messaggio, dovrà sempre aspettare di ricevere la chiave pubblica di Alice
</template>
<style></style>
