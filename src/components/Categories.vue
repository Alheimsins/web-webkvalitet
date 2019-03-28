<template>
  <v-container
    grid-list-md
  >
    <v-layout row wrap>
      <v-flex
        v-for="(category, i) in categories"
        :key="i"
      >
        <v-card flat>
          <v-card-text class="text-xs-center">
            <p style="white-space: nowrap;">{{ category.title }}</p>
            <v-tooltip bottom>
              <template v-slot:activator="{ on }">
                <v-progress-circular
                  v-on="on"
                  :color="color(category.score)"
                  :value="category.score"
                  size="50"
                >
                  {{ category.score }}
                </v-progress-circular>
              </template>
              <span>{{ category.description || 'None' }}</span>
            </v-tooltip>
          </v-card-text>
        </v-card>
      </v-flex>
    </v-layout>
  </v-container>
</template>

<script>
export default {
  props: {
    categories: Array
  },
  methods: {
    color (score) {
      if (score >= 90) {
        return '#18b663'
      }
      if (score >= 50) {
        return '#fb8c00'
      }
      return '#e53935'
    }
  }
}
</script>
