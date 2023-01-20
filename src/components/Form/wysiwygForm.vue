<template>
   <div class="box" :class="ClassStyle">
      <label>{{ name }}</label>
      <q-editor v-model="editor" min-height="5rem" :rules="validations" />
   </div>
</template>

<script>
import { defineComponent } from "vue";
import { ref } from "vue";

export default defineComponent({
   data() {
      return {
         editor: ref(this.values),
         newValue: "",
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
   mounted() {
      this.newValue = this.values;
      if (this.ui) {
         for (const [key, value] of Object.entries(this.ui)) {
            this.ClassStyle = `${key}-${value}`;
         }
      }
   },
});
</script>
