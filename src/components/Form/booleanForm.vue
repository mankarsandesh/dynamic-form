<template>
   <div class="box" :class="ClassStyle">
      <label>{{ name }}</label>
      <q-toggle color="green" v-model="newValue" :rules="validations" /> <br />
      <small>{{ description }}</small>
   </div>
</template>

<script>
import { defineComponent } from "vue";
export default defineComponent({
   name: "booleanForm",
   data() {
      return {
         newValue: false,
         ClassStyle: "col-12",
      };
   },
   props: {
      name: {
         type: Object,
      },
      description: {
         type: String,
      },
      placeholder: {
         type: String,
      },
      default: {
         type: String,
      },
      validations: {
         type: Array,
      },
      values: {
         type: Boolean,
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
      if (this.values) {
         this.newValue = this.values == "1" ? true : false;
      } else {
         this.newValue = this.default == "1" ? true : false;
      }
      if (this.ui) {
         for (const [key, value] of Object.entries(this.ui)) {
            this.ClassStyle = `${key}-${value}`;
         }
      }
   },
});
</script>
<style>
.box {
   padding: 10px;
}
</style>
