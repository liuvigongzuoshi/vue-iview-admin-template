<template>
  <div class="dashboard">
    <PanelGroup :data="panelData" />
    <i-row class="dashboard__multi-chart" :gutter="32">
      <i-col :xs="24" :sm="24" :lg="8">
        <RaddarChart class="dashboard__chart-wrapper" />
      </i-col>
      <i-col :xs="24" :sm="24" :lg="8">
        <PieChart class="dashboard__chart-wrapper" />
      </i-col>
      <i-col :xs="24" :sm="24" :lg="8">
        <BarChart class="dashboard__chart-wrapper" />
      </i-col>
    </i-row>
    <i-card class="dashboard__line-chart" shadow>
      <LineChart :chart-data="lineChartData" />
    </i-card>
  </div>
</template>

<script>
import echarts from 'echarts/lib/echarts'
import chartTheme from '@/themes/chart-theme'
import PanelGroup from './components/PanelGroup'
import LineChart from './components/LineChart'
import RaddarChart from './components/RaddarChart'
import PieChart from './components/PieChart'
import BarChart from './components/BarChart'
import { getSysLogCountApi } from '@/api/dashboard'

echarts.registerTheme('chartTheme', chartTheme)

export default {
  name: 'Dashboard',

  components: {
    PanelGroup,
    LineChart,
    RaddarChart,
    PieChart,
    BarChart
  },

  filters: {},

  props: {},

  data() {
    return {
      panelData: [
        { title: 'Online', icon: 'md-globe', count: 0, color: '#2d8cf0' },
        { title: 'New Visits', icon: 'md-people', count: 0, color: '#9A66E4' },
        { title: 'Total User', icon: 'md-stats', count: 0, color: '#19bef0' },
        { title: 'Messages', icon: 'md-text', count: 0, color: '#facc14' }
      ],
      lineChartData: {
        expectedData: [140, 192, 120, 144, 160, 130, 140],
        actualData: [40, 160, 151, 106, 145, 150, 130]
      }
    }
  },

  computed: {},

  watch: {},

  created() {
    getSysLogCountApi().then(data => {
      let { online, newVisits, totalUser, messages } = data
      let inforCount = [online, newVisits, totalUser, messages]
      this.panelData = this.panelData.map((item, index) => {
        return { ...item, count: inforCount[index] }
      })
    })
  },

  mounted() {},

  updated() {},

  activated() {},

  deactivated() {},

  beforeDestroy() {},

  destroyed() {},

  methods: {}
}
</script>

<style lang="less">
.dashboard {
  &__line-chart {
    margin-top: 20px;
  }

  &__multi-chart {
    margin-top: 20px;
  }

  &__chart-wrapper {
    padding: 10px 10px 0;
    background: #fff;
  }
}
</style>
