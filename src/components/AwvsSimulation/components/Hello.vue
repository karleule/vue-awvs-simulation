<template>
  <v-card style="width: 552px; height:312px;">
      <v-card-text  style="width: 552px; height:260px;">
        <div class="subheading">        
          Hallo, <br>
          auf dieser Seite können Sie an einer "Simulation zum Anweisungsverständnis im Störlärm" teilnehmen.
          Die Simulation beginnen Sie mit einem Klick auf den "Start"-Button.
          Danach hören Sie eine Lehrerin, die ihrer Klasse Anweisungen gibt.
          Bitte folgen auch Sie diesen Anweisungen.
          Die Anweisungen dauern fast zwei Minuten.
          Danach können sie auf den unten rechts erscheinenden Button ("Karten umdrehen") klicken.
          Vergleichen Sie zum Schluss Ihr Ergebnis
        </div>
      </v-card-text>
    <v-card-actions>
      <v-btn style="background: #5A2572; color: white;" @click="$emit('start')">
        Start
      </v-btn>
    </v-card-actions>
  </v-card>
</template>
