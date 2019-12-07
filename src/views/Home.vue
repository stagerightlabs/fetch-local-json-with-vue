<template>
  <div class="home">
    <div v-if="loaded">
      <h2>{{ dataSetName }}</h2>
      <h3>https://catalog.data.gov/dataset/pm2-5-air-quality-standard-update</h3>
      <div v-for="complaint in filteredData" :key="complaint[1]">
        <p style="margin-bottom: 20px; text-align:justify">
          {{ complaint[13] }}
          <br />
          - {{ complaint[8] }} {{ complaint[9] }}
        </p>
      </div>
    </div>
    <p v-else>Loading...</p>
  </div>
</template>

<script>

export default {
  name: 'home',
  data () {
    return {
      airData: {},
      loaded: false
    }
  },
  computed: {
    filteredData () {
      return this.airData.data.filter(d => d[13])
    },
    dataSetName () {
      return this.airData.meta.view.name
    }
  },
  methods: {
    getJsonData () {
      fetch('air_quality.json')
        .then(response => response.json())
        .then(data => {
          this.airData = data
          this.loaded = true
        })
    }
  },
  mounted () {
    this.getJsonData()
  }
}
</script>
