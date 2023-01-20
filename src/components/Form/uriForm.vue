<template>
   <div class="box" :class="ClassStyle">
      <q-input
         filled
         :label="name"
         placeholder="placeholder"
         lazy-rules
         :rules="validations"
         v-model="newValue"
      />
   </div>
</template>

<script>
import { defineComponent } from "vue";

export default defineComponent({
   name: "uriForm",
   data() {
      return {
         newValue: this.values,
         ClassStyle: "col-12",
      };
   },
   props: {
      name: {
         type: Object,
      },
      validations: {
         type: Array,
      },
      values: {
         type: String,
      },
      ui: {
         type: Object,
      },
      multiple_min: {
         type: String,
         default: null,
      },
      multiple_max: {
         type: String,
         default: null,
      },
   },
});
</script>
<style>
.box {
   padding: 10px;
}
</style>
