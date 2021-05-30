<template>
  <div id="app">
    <div class="header">
      <img alt="Vue logo" src="./assets/logo.png">
      <h1>Task 1 Vue</h1>
    </div>
    <div class="header">
      <button @click="showJson">
        Показать JSON
      </button>
      <button @click="removeChanges">
        Отменить изменения
      </button>
    </div>
    <ul>
      <span :style="changeVisualTreeElemState()">
      {{ initialJson['name'] }}
      </span>
      <TreeCatalog
          v-for="(elem, index) in initialJson['catalog']"
          :initialJson="elem"
          :key="index"
      />
    </ul>
    <div v-if="showCurrentJSON">
      <pre>
        {{ visualJson }}
      </pre>
    </div>
  </div>
</template>

<script>
import TreeCatalog from "@/components/TreeCatalog";
import initJson from "./tree.json"

export default {
  name: 'App',
  data() {
    return {
      initialJson: initJson,
      visualJson: initJson,
      showCurrentJSON: false,
    }
  },
  components: {
    TreeCatalog
  },

  methods: {
    showJson() {
      this.showCurrentJSON ? this.showCurrentJSON = false : this.showCurrentJSON = true;
    },

    /**
     * Функция, изменяющая состояние элемента, которое зависит от количества вложенных выделенных элементов
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

  },

    removeChanges() {
      this.initialJson = this.visualJson
    }
  }
}
</script>

<style>
.header {
  text-align: center;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: left;
  color: #2c3e50;
  margin-top: 60px;

}
</style>
