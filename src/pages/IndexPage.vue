<template>
   <q-page-container class="box BlockTitle">
      <div class="row">
         <div class="col-4 bg-blue-grey-1 leftBoxBlock">
            <p class="q-pa-sm">Click Blocks and Add Block to Form</p>
            <q-card
               class="my-card"
               v-for="(data, index) in FormData"
               :key="index"
               @click="addBlock(data)"
               >{{ index + 1 }} . {{ data.name }}</q-card
            >
            <div class="q-pa-sm q-gutter-sm">
               <q-btn
                  push
                  color="primary"
                  label="Clear Form"
                  @click="clearForm"
               />
            </div>
         </div>
         <div class="col-8">
            <div class="border rounded-border rightBox">
               <div v-if="loading">
                  <q-spinner-facebook color="primary" size="2em" />
                  <q-tooltip :offset="[0, 8]">QSpinnerFacebook</q-tooltip>
               </div>
               <p class="q-pa-sm text-blue-5 text-h4" v-if="NewData.length > 0">
                  Articles Form
               </p>

               <div
                  class="row justify-center items-center"
                  style="height: 80vh"
                  v-if="NewData.length == 0"
               >
                  <div class="text-blue-grey-3">There are no blocks</div>
               </div>
               <q-form
                  v-if="NewData.length > 0"
                  class="q-gutter-md"
                  @submit="handleSubmit(onSubmit)"
                  @reset="onReset"
               >
                  <div
                     v-for="(rows, index) in NewData"
                     :key="index"
                     class="blockBox"
                  >
                     <q-card class="my-card flex justify-between">
                        {{ rows.name }}
                        <span
                           class="material-icons text-primary"
                           @click="removeObj(index)"
                        >
                           delete
                        </span>
                     </q-card>
                     <div class="row">
                        <component
                           v-for="(data, indexId) in rows.fields"
                           :key="`molecule1_${indexId}`"
                           :is="`${data.type}Form`"
                           v-model="data.values"
                           v-bind="{
                              ...data,
                           }"
                        >
                        </component>
                     </div>
                  </div>
               </q-form>
            </div>
         </div>
      </div>
   </q-page-container>
</template>

<script>
import schema from '../static/schema.json';
import {
   booleanForm,
   colorForm,
   editorForm,
   stringForm,
   uriForm,
   wysiwygForm,
} from '../components/Form';
import { defineComponent } from 'vue';

export default defineComponent({
   name: 'IndexPage',
   components: {
      booleanForm,
      colorForm,
      editorForm,
      stringForm,
      uriForm,
      wysiwygForm,
   },
   data() {
      return {
         FormData: schema,
         loading: false,
         NewData: [],
      };
   },
   methods: {
      // Clear Form
      clearForm() {
         this.NewData = [];
      },
      // Remove Block from Array
      removeObj(id) {
         this.loading = true;
         const arrCopy = Array.from(this.NewData);
         const objWithIdIndex = arrCopy.findIndex((obj, index) => index === id);
         arrCopy.splice(objWithIdIndex, 1);
         this.NewData = arrCopy;
         this.loading = false;
      },
      // Add Block to Form
      addBlock(object) {
         this.loading = true;
         console.log(object);
         this.NewData.push(object);
         this.loading = false;
      },
      // On Click Submit
      onSubmit() {
         // eslint-disable-next-line
         console.log('Form submitted yay!');
      },
      // Reset Form
      onReset() {
         requestAnimationFrame(() => {
            this.$refs.observer.reset();
         });
      },
   },
});
</script>
<style>
.leftBoxBlock {
   border-radius: 4px;
   padding: 10px 10px;
   height: 100% !important;
   position: -webkit-sticky;
   position: sticky;
   top: 40px;
}
.BlockTitle {
   padding: 8px 14px;
   font-size: 18px;
   margin: 0 auto;
   width: 60%;
}
.my-card {
   padding: 6px 8px;
   margin: 5px 10px;
   cursor: pointer;
}
.blockBox {
   border: 1px solid #dddddd;
   border-radius: 5px;
   padding: 8px 4px;
}
.rightBox {
   padding: 0px 10px;
   border-radius: 5px;
   /* height: 100%; */
}
</style >
