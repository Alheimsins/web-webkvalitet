<template>
  <v-container
    flex
    grid-list-lg
  >
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
        <categories :categories="item.result">
        </categories>
        </card>
      </v-flex>
    </v-layout>
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
    results: []
  }),
  async created () {
    // const { data } = await this.$http.get('https://young-shape-9421.getsandbox.com/')
    const { data } = await this.$http.get('https://webkvalitet.api.service.t-fk.no/')
    const totalScore = categories => categories.reduce((prev, cur) => prev + cur.score, 0)
    const result = data
      .map(item => ({ ...item, total: totalScore(item.result) }))
      .sort((a, b) => (a.total < b.total) ? 1 : -1)
    this.results = result
  }
}
</script>
