<template>
  <q-page padding>
    <h6>New Form</h6>
    <q-form
      :ref="myform"
      @reset="onReset"
      @submit.prevent="onSubmit"
      class="row q-gutter-xs justify-between"
    >
      <div class="col-12 col-sm-6">
        <q-input
          v-model="data.product"
          label="Product"
          lazy-rules
          :rules="[(val) => val.length > 3 || 'Min 3 characters']"
        />
      </div>

      <div class="col-12 col-sm-5">
        <q-select
          v-model="data.priority"
          label="Priority"
          :rules="[(val) => val.length > 0 || 'Select priority']"
          :options="['low', 'medium', 'high']"
        />
      </div>

      <div class="col-12">
        <q-toggle label="Accept Terminos" v-model="data.terminos" />
      </div>

      <div class="col-12 q-gutter-sm q-mt-md">
        <q-btn
          :disable="
            data.product.length <= 3 || !data.priority || !data.terminos
          "
          type="submit"
          text-color="white"
          label="Submit"
          rounded
          color="primary"
          :ripple="false"
          style="min-width: 90px"
        />
        <q-btn
          text-color="white"
          label="Reset"
          rounded
          color="secondary"
          :ripple="false"
          style="min-width: 90px"
          type="reset"
        />
      </div>
    </q-form>

    <TableComponent :rows="products" />
  </q-page>
</template>

<script setup lang="ts">
export type priorityType = 'low' | 'medium' | 'high';
export interface IForm {
  product: string;
  priority: priorityType;
  terminos: boolean;
}
import { ref } from 'vue';
import { useQuasar } from 'quasar';

// refs
const $q = useQuasar();
const data = ref<IForm>({
  product: '',
  priority: 'low',
  terminos: false,
});
import { QForm } from 'quasar';
import TableComponent from 'src/components/TableComponent.vue';
const myform = ref<InstanceType<typeof QForm> | null>(null);
const products = ref<IForm[]>([]);

// methods
const onSubmit = () => {
  $q.notify({
    message: `${data.value.product} created`,
    color: 'positive',
    icon: 'check',
    position: 'bottom',
    timeout: 1000,
  });

  products.value = [...products.value, { ...data.value }];

  myform.value?.resetValidation();
  onReset();
};

const onReset = () => {
  data.value.product = '';
  data.value.priority = 'low';
  data.value.terminos = false;
};
</script>
