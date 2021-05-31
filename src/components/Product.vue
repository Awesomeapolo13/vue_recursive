<template>
  <li>
    <input
        type="checkbox"
        name="selected"
        v-model="initialJson['selected']"
        v-bind:checked="initialJson['selected']"
        @input="changeCheckboxValue(initialJson)">
    {{ initialJson['name'] }}
  </li>
</template>

<script>
export default {
  name: "Product",
  props: ['initialJson'],
  methods: {
    /**
     * Метод изменения данных о выделенности
     */
    changeCheckboxValue(initialJson) {
      event.target.checked ? this.initialJson['selected'] = true : initialJson['selected'] = false;
    },

    /**
     * Метод отображения / скрытия элементов поддерева
     */
    showElements() {
      this.show ? this.show = false : this.show = true;
    }
  },
}
</script>

<style scoped>

</style>