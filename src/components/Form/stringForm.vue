<template>
   <div class="box" :class="ClassStyle">
      <q-input
         filled
         v-model="newValue"
         :label="name"
         lazy-rules
         :hint="description"
         :placeholder="placeholder"
      />
   </div>
</template>

<script>
import { defineComponent } from 'vue';
import { ref } from 'vue';
export default defineComponent({
   data() {
      return {
         newValue: ref(this.values ? this.values : this.default),
         ClassStyle: 'col-12',
      };
   },
   props: {
      name: {
         type: Object,
      },
      default: {
         type: String,
      },
      description: {
         type: String,
      },
      placeholder: {
         type: String,
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
   computed: {
      // validation Rule Don't used Yet
      validationRule: {
         get: function () {
            return this.validations.join('|');
         },
      },
   },
   mounted() {
      // UI Class Append in Style
      if (this.ui) {
         for (const [key, value] of Object.entries(this.ui)) {
            this.ClassStyle = `${key}-${value}`;
         }
      }
   },
});
</script>
