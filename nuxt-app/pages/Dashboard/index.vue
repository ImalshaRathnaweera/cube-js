<template>
  <v-container fluid class="text-center background pa-0">
    <query-builder :cubejs-api="cubejsApi" :query="query" style="width: 100%">
      <template
        v-slot:builder="{
          measures,
          setMeasures,
          availableMeasures,
          dimensions,
          setDimensions,
          availableDimensions,
          segments,
          setSegments,
          availableSegments,
        }"
      >
        <v-container fluid class="pa-4 pa-md-8 pt-6 background-white">
          <v-row>
            <v-col cols="12" md="2">
              <v-select
                multiple
                label="Measures"
                outlined
                hide-details
                :value="measures.map((i) => i.name)"
                :items="availableMeasures.map((i) => i.name)"
                @change="setMeasures"
              />
            </v-col>
            <v-col cols="12" md="2">
              <v-select
                multiple
                label="Dimensions"
                outlined
                hide-details
                :value="dimensions.map((i) => i.name)"
                :items="availableDimensions.map((i) => i.name)"
                @change="setDimensions"
              />
            </v-col>
            <v-col cols="12" md="2">
              <v-select
                multiple
                label="Segments"
                outlined
                hide-details
                :value="segments.map((i) => i.name)"
                :items="availableSegments.map((i) => i.name)"
                @change="setSegments"
              />
            </v-col>
          </v-row>
        </v-container>
      </template>
      <template v-slot="{ resultSet }">
        <!-- <div v-if="resultSet" class="pa-4 pa-md-8">
          <div class="border-light pa-4 pa-md-12">
            <line-chart legend="bottom" :data="series(resultSet)"></line-chart>
          </div>
        </div> -->
        <div v-if="resultSet" class="pa-4 pa-md-8">
          <div class="border-light pa-4 pa-md-12">
            <bar-chart legend="bottom" :chart-data="series2()"></bar-chart>
          </div>
        </div>
        <!-- <div v-if="resultSet" class="pa-4 pa-md-8">
          <div class="border-light pa-4 pa-md-12">
            <area-chart
              legend="bottom"
              :data="series(resultSet)"
              background-color="white"
            ></area-chart>
          </div>
        </div> -->
        <!-- <div v-if="resultSet" class="pa-4 pa-md-8">
          <div class="border-light pa-4 pa-md-12">
            <pie-chart
              legend="bottom"
              :data="datasets"
              :donut="true"
            ></pie-chart>
          </div>
        </div> -->
      </template>
    </query-builder>
  </v-container>
</template>

<script>
import cubejs from '@cubejs-client/core'
import { QueryBuilder } from '@cubejs-client/vue'
// import LineChart from '~components/LineChart.js'
import BarChart from '~/components/BarChart.js'
// import AreaChart from '~components/AreaChart'

const cubejsApi = cubejs('SILENT', {
  apiUrl: `http://localhost:4000/cubejs-api/v1`,
})

export default {
  components: {
    QueryBuilder,
    BarChart,
    // LineChart,
  },
  data: () => {
    const query = {
      limit: 100,
    }

    return {
      cubejsApi,
      query,
      datasets: [
        ['hdfghj', 20],
        ['Feb', 10],
        ['jsks', 34],
        ['iucjwbcjd', 78],
      ],
    }
  },
  methods: {
    series(resultSet) {
      // console.log(resultSet)
      return resultSet.series().map((series) => ({
        name: series.key, // dimesion name or masurer name
        data: series.series.map((row) => [row.x, row.value]),
      }))
    },
    series2() {
      return {
        labels: this.resultSet.series2().data.row.x, // x axies   this.resultSet.
        datasets: [
          {
            label: '# of Votes', // dimesion or masurer name
            data: [12, 19, 3, 5, 2, 3], // y axies
            backgroundColor: [
              'rgba(255, 99, 132, 0.2)',
              'rgba(54, 162, 235, 0.2)',
              'rgba(255, 206, 86, 0.2)',
              'rgba(75, 192, 192, 0.2)',
              'rgba(153, 102, 255, 0.2)',
              'rgba(255, 159, 64, 0.2)',
            ],
            borderColor: [
              'rgba(255, 99, 132, 1)',
              'rgba(54, 162, 235, 1)',
              'rgba(255, 206, 86, 1)',
              'rgba(75, 192, 192, 1)',
              'rgba(153, 102, 255, 1)',
              'rgba(255, 159, 64, 1)',
            ],
            borderWidth: 1,
          },
        ],
      }
    },
  },
}
</script>

<style scopped>
.background {
  background: #f3f3fb;
  min-height: 100vh;
}
.background-white {
  background: #fff;
}
.border-light {
  background: #ffffff;
  border-radius: 8px;
}
</style>
