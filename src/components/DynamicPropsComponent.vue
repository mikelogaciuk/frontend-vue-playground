<template>
  <div>
    <br />
    <p>This is a dynamic props component.
      <br />
      It receives the following stats:
    </p>
    <br />
    <div class="d-stats bg-base-100 border-base-200 rounded-xs border">
      <div class="d-stat">
        <div class="d-stat-title">Sales</div>
        <div class="d-stat-value">{{ props.sales.toLocaleString('en-US', { style: 'currency', currency: 'USD' }) }}
        </div>
      </div>
      <div class="d-stat text-secondary">
        <div class="d-stat-title">Revenue</div>
        <div class="d-stat-value">{{ props.revenue.toLocaleString('en-US', { style: 'currency', currency: 'USD' }) }}
        </div>
      </div>
      <div class="d-stat">
        <div class="d-stat-title">Profit</div>
        <div class="d-stat-value">{{ props.profit.toLocaleString('en-US', { style: 'currency', currency: 'USD' }) }}
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
const props = defineProps(['sales', 'revenue', 'profit']);

</script>

<style></style>
