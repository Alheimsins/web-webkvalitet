<template>
  <v-container
    flex
    grid-list-lg
  >
    <v-dialog
      v-model="loading"
      hide-overlay
      persistent
      lazy
      width="300"
    >
      <v-card
        color="black"
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
    <v-layout
      column
      wrap
      align-center
      justify-center
    >
      <v-flex v-for="(item, i) in results" :key="i">
        <card
          :name="item.name"
          :url="item.url"
          :report-url="'https://lighthouse-dot-webdotdevsite.appspot.com/lh/html?url=' + item.url"
          :number="++i"
          :date="item.date"
        >
          <categories :categories="item.result"></categories>
        </card>
      </v-flex>
    </v-layout>

    <v-snackbar v-model="snackbar.active" :color="snackbar.type === 'error' ? 'error' : 'primary'" :bottom="true">
      {{snackbar.message}}
    </v-snackbar>
  </v-container>
</template>

<script>
import card from '@/components/Card'
import categories from '@/components/Categories'

export default {
  components: {
    card,
    categories
  },
  data: () => ({
    results: [],
    loading: true,
    snackbar: {
      active: false,
      message: false,
      type: false
    }
  }),
  methods: {
    notification (msg, type = 'info') {
      this.snackbar.message = msg
      this.snackbar.type = type
      this.snackbar.active = true
    }
  },
  async created () {
    try {
      const { data } = await this.$http.get('https://webkvalitet.api.service.t-fk.no/')
      const totalScore = categories => categories.reduce((prev, cur) => prev + cur.score, 0)
      this.results = data
        .map(item => ({ ...item, categories: item.result.sort((a, b) => a.title.localeCompare(b.title)), total: totalScore(item.result) }))
        .sort((a, b) => (a.total < b.total) ? 1 : -1)
      this.loading = false
    } catch (error) {
      console.log(error)
      this.notification('Could not get data from API', 'error')
      this.loading = false
    }
  }
}
</script>
