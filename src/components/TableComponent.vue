<template>
  <q-table
    title="Products"
    class="q-mt-md"
    :columns="columns"
    :rows="rows"
    no-data-label="No hay productos"
  />
</template>
<script setup lang="ts">
import { IForm } from '../pages/FormPage.vue';
import { PropType } from 'vue';

defineOptions({
  name: 'TableComponent',
});
defineProps({
  rows: {
    type: Array as PropType<IForm[]>,
    required: true,
  },
});

const columns = [
  {
    name: 'product',
    label: 'Product',
    align: 'left' as const,
    field: 'product',
    sortable: true,
  },
  {
    name: 'priority',
    label: 'Priority',
    align: 'left' as const,
    field: 'priority',
    sortable: true,
  },
];
</script>
<style></style>
