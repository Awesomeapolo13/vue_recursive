<template>
  <li v-if="initialJson['catalog'] !== undefined">
    <button @click="showElements()">{{ show ? '-' : '+' }}</button>
    <input
        type="checkbox"
        name="selected"
        :checked="initialJson['selected']"

        @input="getCheckboxValue(initialJson)">
    {{ initialJson['name'] }}
    <ul v-if="show">
      <TreeCatalog
          v-for="(elem, index) in initialJson['catalog']"
          :initialJson="elem"
          :key="index"
          :show="false"
      />
    </ul>
  </li>
  <Product
      v-else
      :initialJson="initialJson"

  />
</template>

<script>
import Product from "@/components/Product";
import Checkbox from "@/components/Checkbox";

export default {
  name: "TreeCatalog",
  props: ['initialJson', 'visualJson', 'show', 'elem'],
  components: {Checkbox, Product},
  showItem: false,
  comments: {
    Product,
  },
  // data() {
  //   return {
  //     checkState: this.initialJson['selected']
  //   }
  // },
  methods: {
    getCheckboxValue(initialJson) {
      if (event.target.checked) {
        initialJson['selected'] = true;
        console.log('checked', initialJson['selected']);
      } else {
        initialJson['selected'] = false;
        console.log('unchecked', initialJson['selected']);
      }

    },
    showElements() {
      this.show ? this.show = false : this.show = true;
    }
  },
  computed: {
    // setCheckbox() {
    //   let checkbox = document.querySelector('.checkbox')
    //   if (show) {
    //     checkbox.checked = true;
    //   } else {
    //     checkbox.checked = false;
    //   }
    // }
  }
}
</script>

<style scoped>

</style>