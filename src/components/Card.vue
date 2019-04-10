<template>
  <v-card>
    <v-toolbar dark color="black">
        <v-toolbar-title>
          <v-avatar size="32" color="white">
            <span class="black--text headline">{{ number }}</span>
          </v-avatar>
          {{ name }}
        </v-toolbar-title>
        <v-spacer></v-spacer>

        <v-tooltip bottom>
          <template v-slot:activator="{ on }">
            <a v-on="on" :href="url" rel="noopener" target="_blank" aria-label="Gå til nettside">
              <v-icon>link</v-icon>
            </a>
          </template>
          <span>Gå til {{ url }}</span>
        </v-tooltip>
        &nbsp;
        <v-tooltip bottom>
          <template v-slot:activator="{ on }">
            <a v-on="on" :href="reportUrl" rel="noopener" target="_blank" aria-label="Gå til rapport fra Lighthouse">
              <v-icon>remove_red_eye</v-icon>
            </a>
          </template>
          <span>Se Lighthouse rapport</span>
        </v-tooltip>
        &nbsp;
        <v-tooltip bottom>
          <template v-slot:activator="{ on }">
            <a v-on="on" :href="observatoryUrl" rel="noopener" target="_blank" aria-label="Gå til rapport fra Observatory">
              <v-icon>remove_red_eye</v-icon>
            </a>
          </template>
          <span>Se Observatory rapport</span>
        </v-tooltip>
    </v-toolbar>
    <v-container
      grid-list-md
    >
      <v-layout row wrap>
        <slot></slot>
      </v-layout>
      <p class="text-xs-center font-italic">Sist oppdatert {{ new Date(date).toLocaleString() }}</p>
    </v-container>
  </v-card>
</template>

<script>
export default {
  props: {
    name: String,
    number: Number,
    url: String,
    reportUrl: String,
    observatoryUrl: String,
    date: String
  }
}
</script>
