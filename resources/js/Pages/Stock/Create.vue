<template>
  <div>
    <Layout>
      <div class="flex justify-center">
        <div class="bg-white flex flex-col w-1/3 mt-20 p-6">
          <h2 class="text-lg">Stock Form</h2>
          <form action="" id="stock-form" name="stock-form" v-on:submit.prevent="submit">
            <div class="flex flex-col pt-6">
              <label for="id">ID</label>
              <input type="text" id="id" name="id" v-model="form.id" autocomplete="off"/>
              <div class="text-red-700 text-sm">{{errors.id}}</div>
            </div>

            <div class="flex flex-col pt-6">
              <label for="description">Description</label>
              <input type="text" id="description" name="description" v-model="form.description" autocomplete="off"/>
              <div class="text-red-700 text-sm">{{errors.description}}</div>
            </div>

            <div class="flex flex-col pt-6">
              <label for="stock_category_id">Stock Category ID</label>
              <select name="type" id="stock_category_id">
                  <option v-for="item in stock_categories" v-bind:value="item.id" v-model="form.stock_category_id">{{item.id}}</option>
              </select>
              <div class="text-red-700 text-sm">{{errors.stock_category_id}}</div>
            </div>

            <div class="flex flex-col pt-6">
              <label for="uom">Uom</label>
              <input type="text" id="uom" name="uom" v-model="form.uom" autocomplete="off"/>
              <div class="text-red-700 text-sm">{{errors.uom}}</div>
            </div>

                    <!-- 'id','description','stock_category_id','uom','barcode',
        'discontinued',
        'photo_path' -->

            <div class="flex flex-col pt-6">
              <label for="barcode">Barcode</label>
              <input type="text" id="barcode" name="barcode" v-model="form.barcode"/>
              <div class="text-red-700 text-sm">{{errors.barcode}}</div>
            </div>

            <div class="flex flex-col pt-6">
              <label for="discontinued">Discontinued</label>
              <div class="flex flex-row">
                    <input type="radio" class="mr-6" id="discontinued1" name="discontinued" value="Y" v-model="form.discontinued"/>
                    <label for="yes" > Yes</label><br>
                </div>
                <div class="flex flex-row">
                    <input type="radio" class="mr-6" id="discontinued2" name="discontinued" value="N" v-model="form.discontinued">
                    <label for="no" > No</label><br>
                </div>
              
              <div class="text-red-700 text-sm">{{errors.discontinued}}</div>
            </div>

            <div class="flex flex-col pt-6">
                <button type="submit" class="bg-indigo-800 text-white p-2">Save</button>
            </div>
          </form>
        </div>
      </div>
    </Layout>
  </div>
</template>

<script>
import { ref, reactive } from "vue";
import Layout from "@/Layouts/Authenticated";
import { Inertia } from "@inertiajs/inertia";

export default {
  components: {
    Layout,
  },
  props:{
      errors: Object,
      stock_categories: Array,

  },
  setup(props, context) {

      const form = reactive({
          id:null,
          description:null,
          stock_category_id: 1539,
          uom:null,
          barcode:null,
          discontinued: "Y",
          photo_path:null
      });

    //   'id',
    //     'description',
    //     'stock_category_id',
    //     'uom',
    //     'barcode',
    //     'discontinued',
    //     'photo_path'

      const submit = () => {
          Inertia.post(route("stock.store"),form
        //   ,{
        //       onSuccess: () => {
        //             form.id = null;
        //             form.description = null
        //             form.stock_category_id = 1539
        //             form.uom = null;
        //             form.barcode = null;
        //             form.discontinued =  "Y";
        //       }
        //   }
          );
      };
    return {
        form,
        submit,
    };
  },
};
</script>

<style>
</style>