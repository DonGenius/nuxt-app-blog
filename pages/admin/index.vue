<template>
  <section>
    <h1>admin panel</h1>
    <app-analytics-chart
      title="Views"
      :labels="views.labels"
      :data="views.data"
    ></app-analytics-chart>
    <app-analytics-chart
      title="Comments"
      :labels="comments.labels"
      :data="comments.data"
    ></app-analytics-chart>
  </section>
</template>

<script>
  import AppAnalyticsChart from '../../components/admin/AnalyticsChart'
  export default {
    layout: 'admin',
    components: {
      AppAnalyticsChart
    },
    middleware: ['admin-auth'],
    name: "index",
    async asyncData({store}) {
      const {views, comments} = await store.dispatch('post/getAnalytics')
      return {views, comments}
    },
  }
</script>

<style scoped>

</style>
