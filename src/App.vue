<template>

  <v-app>

    <v-main>

      <v-container>

        <v-card>

          <v-card-title>

            <h1>KaufDeinAuto.de</h1>

          </v-card-title>

          <v-card-text>

            <v-row>

              <v-col cols="4">

                <v-text-field v-model="brand" label="Marke"></v-text-field>

              </v-col>

              <v-col cols="4">

                <v-text-field v-model="model" label="Modell"></v-text-field>

              </v-col>

              <v-col cols="4">

                <v-text-field v-model="imageLink" label="Bild-Link"></v-text-field>

              </v-col>

            </v-row>

          </v-card-text>

          <v-card-actions>

            <v-btn @click="addCar" color="primary">Auto hinzufügen</v-btn>

            <v-btn @click="showCars" color="secondary">Autos anzeigen</v-btn>

          </v-card-actions>

        </v-card>

 

        <v-card v-for="(car, index) in cars" :key="index" :style="{ display: car.display ? 'block' : 'none' }">

          <v-card-title>

            {{ car.brand }}

          </v-card-title>

          <v-card-subtitle>

            {{ car.model }}

          </v-card-subtitle>

          <v-card-text>

            <img :src="car.imageLink" alt="Car Image" width="300" height="180">

          </v-card-text>

        </v-card>

 

        <v-alert v-if="duplicateError" type="error">

          Hier ist ein Fehler aufgetreten. Dieses Auto existiert bereits.

        </v-alert>

      </v-container>

    </v-main>

  </v-app>

</template>

 

<script>

export default {

  data() {

    return {

      brand: '',

      model: '',

      imageLink: '',

      cars: [],

      duplicateError: false,

    };

  },

  methods: {

    addCar() {

      // Überprüfe, ob ein Auto mit denselben Marke und Modell-Daten bereits existiert

      const isDuplicate = this.cars.some(car => car.brand === this.brand && car.model === this.model);

 

      if (isDuplicate) {

        this.duplicateError = true;

      } else {

        // Wenn kein Duplikat gefunden wurde, füge das Auto zur Liste hinzu

      this.cars.forEach(car => {

        car.display = true;

      });

 

        const newCar = {

          brand: this.brand,

          model: this.model,

          imageLink: this.imageLink,

          display: true, // Anfangs werden alle Karten angezeigt

        };

        this.cars.push(newCar);

 

     

       

 

        // Nach dem Hinzufügen leeren wir die Eingabefelder und setzen den Fehler zurück

        this.brand = '';

        this.model = '';

        this.imageLink = '';

        this.duplicateError = false;

      }

    },

 

    showCars() {

      // Hier blenden wir alle Karten aus und wieder ein

      this.cars.forEach(car => {

        car.display = !car.display;

      });

    },

  },

};

</script>

 

<style scoped>

/* Füge hier ggf. benutzerdefinierte CSS-Stile hinzu */

</style>

 