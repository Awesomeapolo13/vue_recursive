<template>
  <li>
    <input
        type="checkbox"
        name="selected"
        v-model="initialJson['selected']"
        v-bind:checked="initialJson['selected']"
        @input="getCheckboxValue(initialJson)">
    {{ initialJson['name'] }}
  </li>
</template>

<script>
export default {
  name: "Product",
  props: ['initialJson'],
  methods: {
    getCheckboxValue(initialJson) {
      // event.target.checked ? this.initialJson['selected'] = true : initialJson['selected'] = false;
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
}
</script>

<style scoped>

</style>