<template>
   <div class="box" :class="ClassStyle">
      <q-input
         filled
         v-model="secondColor"
         :rules="validations"
         :hint="description"
         class="my-input"
      >
         <template v-slot:append>
            <q-icon name="colorize" class="cursor-pointer">
               <q-popup-proxy
                  cover
                  transition-show="scale"
                  transition-hide="scale"
               >
                  <q-color v-model="secondColor" />
               </q-popup-proxy>
            </q-icon>
         </template>
      </q-input>
   </div>
</template>

<script>
import { defineComponent } from "vue";
import { ref } from "vue";
export default defineComponent({
   name: "colorForm",
   data() {
      return {
         color: ref("#FF00FF"),
         secondColor: ref("#027be3"),
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
