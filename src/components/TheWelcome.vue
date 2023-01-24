<script setup>
import { ref, computed } from 'vue';

const products = ref([]);

var summe = 0;
var gpreis = 0;

function increase(index) {
  this.filter[index].Anzahl++;
  summe++;
  gpreis = gpreis + parseFloat(this.filter[index].PreisBrutto)
  gpreisround = Math.round(gpreis * 100) / 100;
}

var gpreisround = 0;


async function fetchData() {
  axios.get('https://ivm108.informatik.htw-dresden.de/ewa/g20/Praktikum/get1.php').then(response => (products.value = response.data));
}

fetchData()

var search = ref('');

const filter = computed(() => {
  return toggle.value
    ? products.value.filter((item) => item.Produkttitel == search.value)
    : products.value

})

const toggle = ref(false);

const show = ref(false)

const showtable = ref(true)

function checkout() {
  show.value = !show.value
  showtable.value = !showtable.value
}
</script>

<template>

  <div id="app">
    <h1>Buchshop - G20 </h1>
    <br />
    <input class="suche" v-model="search" placeholder="Geben Sie den Buchtitel ein">
    <button class="suchebutton" @click="toggle = !toggle">
      {{ toggle? 'Zeige alle Buecher': 'Suchen' }}</button>

    <table v-if="!toggle">
      <tr>
        <th>Buchtitel</th>
        <th>Autor</th>
        <th>Preis</th>
      </tr>
      <tr v-for="product in products">
        <td>{{ product.Produkttitel }}</td>
        <td>{{ product.Autorname }}</td>
        <td>{{ product.PreisBrutto }}</td>
      </tr>
    </table>

    <table v-if="toggle">
      <tr>
        <th>Buchtitel</th>
        <th>Autor</th>
        <th>Preis</th>
      </tr>
      <tr v-for="(product, index) in filter">
        <td>{{ product.Produkttitel }}</td>
        <td>{{ product.Autorname }}</td>
        <td>{{ product.PreisBrutto }}</td>
        <button class="bestellen" @click=increase(index)>Bestellen</button>
        <p class="anzahl">{{ product.Anzahl }}</p>
      </tr>
    </table>

    <div v-if="toggle">
      <button class="warenkorb" @click="checkout">Warenkorb anzeigen</button>
    </div>
    <table class="tablecheckout" v-if="show">
      <tr>
        <th>Buchtitel</th>
        <th>Preis</th>
        <th>Anzahl</th>
      </tr>
      <tr v-for="(item, index) in filter">
        <td>{{ item.Produkttitel }}</td>
        <td>{{ item.PreisBrutto }}</td>
        <td>{{ item.Anzahl }}</td>
        <a :href="'https://ivm108.informatik.htw-dresden.de/ewa/g20/Praktikum/stripe/stripe_redirect.php?live=0' + '&price=' + item.PreisBrutto
        + '&name=' + item.Produkttitel + '&desc=' + item.Kurzinhalt + '&quantity=' + item.Anzahl">
          Checkout</a>
      </tr>
    </table>
    <table class="tablesumme" v-if="show">
      <tr>
        <th>Gesamtzahl Buecher</th>
        <th>Gesamtpreis in €</th>
      </tr>
      <tr>
        <td>{{ summe }}</td>
        <td>{{ gpreisround }}</td>
      </tr>
    </table>
  </div>
</template>

<style>
.tablecheckout {
  width: 51.5%;
}

.tablesumme {
  width: 40%;
  padding: 5px;
  margin: 15px;
  border: 10px;
}

.warenkorb {

  text-align: center;
  padding: 5px;
  margin: 15px;
  width: 15%;

}

h1 {
  margin: auto;
}

th {
  border: 2px solid #04AA6D;
  padding: 20px;
  text-align: center;
  background-color: #04AA6D;
  color: white;
  width: 33%;
}

td {
  border: 2px solid #00bd7e;
  border-collapse: collapse;
  text-align: center;
  padding: 20px;
  width: 33%;
}

a {
  text-align: center;
  padding: 20px;
  width: 33%;
  margin: auto;
}

table {

  border-collapse: collapse;
  text-align: center;
  padding: 10px;
  width: 100%;
}

.bestellen {

  text-align: center;
  padding: 5px;
  margin: 10px;
  width: 100%;

}

.anzahl {
  border: 1px solid #00bd7e;
  text-align: center;
  padding: 2px;
  margin: 10px;
  width: 30%;
  border-radius: 25px;

}

.suche {
  text-align: center;
  padding: 5px;
  margin: 20px;
}

.suchebutton {

  text-align: center;
  padding: 5px;
  margin: 15px;
  width: 15%;
}
</style>