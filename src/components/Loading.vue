<template>
  <v-dialog
    v-model="loading"
    hide-overlay
    persistent
    lazy
    width="300"
  >
    <v-card
      color="primary"
      dark
    >
      <v-card-text>
        Vennligst vent
        <v-progress-linear
          indeterminate
          color="white"
          class="mb-0"
        ></v-progress-linear>
      </v-card-text>
    </v-card>
  </v-dialog>
</template>

<script>
export default {
  props: {
    loading: Boolean
  }
}
</script>
