<template>
  <div class="home">
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
</template>

<script>

export default {
  name: 'home',
  data () {
    return {
      /*eslint-disable */
      airData: AIRQUALITY,
      /* eslint-enable */
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
  }
}
</script>
