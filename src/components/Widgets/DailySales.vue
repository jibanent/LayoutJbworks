<template>
  <app-card
    app-card-class="h-100"
    custom-classes="gradient-pink h-100"
    content-custom-class="d-flex justify-content-between flex-column h-100 chart-card"
  >
    <h5 class="mb-20">{{ $t('message.dailySales') }}</h5>
    <div class="d-flex align-items-end">
      <div class="w-50 chart-content">
        <h2 class="card-count mb-15">
          <count-up :start-val="0" :end-val="42" :decimals="0" :duration="10" />%
        </h2>
        <p class="m-0 card-status">{{ $t('message.salesToday') }}</p>
      </div>
      <div class="w-50  app-chart">
        <daily-sales-mini-chart :width="160" :height="100" />
      </div>
    </div>
  </app-card>
</template>
<script>
import DailySalesMiniChart from 'Components/Charts/DailySalesMiniChart'

export default {
  components: {
    DailySalesMiniChart
  }
}
</script>
