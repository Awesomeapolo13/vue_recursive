<template>
  <li>
    <input
        type="checkbox"
        name="selected"
        v-model="initialJson['selected']"
        v-bind:checked="initialJson['selected']">
    {{ initialJson['name'] }}
  </li>
</template>

<script>
export default {
  name: "Product",
  props: ['initialJson']
}
</script>

<style scoped>

</style>