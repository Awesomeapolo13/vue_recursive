<template>
  <li v-if="initialJson['catalog'] !== undefined">
    <button @click="showElements()">
      {{ newShow ? '-' : '+' }}
    </button>
    <input
        type="checkbox"
        name="selected"
        :checked="initialJson['selected']"
        v-model="initialJson['selected']"
        @input="changeCheckboxValue(initialJson)">
    <span :style="changeVisualTreeElemState()">
      {{ initialJson['name'] }}
    </span>
    <ul v-if="newShow">
      <TreeCatalog
          v-for="(elem, index) in initialJson['catalog']"
          :initialJson="elem"
          :key="index"
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

export default {
  name: "TreeCatalog",
  props: {
    initialJson: Object,
    show: {
      type: Boolean,
      default: false,
    },
  },

  data() {
    return {
      newShow: this.show,
    }
  },
  components: {Product},
  comments: {
    Product,
  },

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
      this.newShow ? this.newShow = false : this.newShow = true;
    },

    /**
     * Метод, изменяющий состояние элемента, которое зависит от количества вложенных выделенных элементов
     * @returns {{color: string}}
     */
    changeVisualTreeElemState() {
      // количество выделенных чекбоксов
      let checkCount = 0;
      // счетчик итераций
      let i = 0;
      // считаем сколько чесбоксов выделено
      for (let item of this.initialJson['catalog']) {
        if (item.selected) {
          checkCount++;
        }
        i++;
      }
      // если все дочерние чекбоксы пусты
      if (checkCount === 0 && i === this.initialJson['catalog'].length) {
        return {
          'color': 'firebrick',
        }
      }
      // если все дочерние чекбоксы выделены
      if (checkCount === this.initialJson['catalog'].length) {
        return {
          'color': 'forestgreen',
        }
      }
    }
  },
}
</script>

<style scoped>

</style>