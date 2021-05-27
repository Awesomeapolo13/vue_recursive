<template>
  <div id="app">
    <div class="header">
      <img alt="Vue logo" src="./assets/logo.png">
      <h1>Task 1 Vue</h1>
    </div>
    <ul>
      {{ initialJson['name'] }}
      <TreeCatalog
          v-for="(elem, index) in initialJson['catalog']"
          :initialJson="elem"
          :key="index"
          :show="false"
      />
    </ul>
    <div>
      <pre>
        <VisualCatalog
            v-for="(elem, index) in visualJson['catalog']"
            :initialJson="elem"
            :key="index"
        />
        {{ visualJson }}
      </pre>
    </div>
  </div>
</template>

<script>
import TreeCatalog from "@/components/TreeCatalog";
import initJson from "./tree.json"
import VisualCatalog from "@/components/VisualCatalog";
export default {
  name: 'App',
  data() {
    return {
      initialJson: initJson,
      visualJson: initJson
    }
  },
  components: {
    VisualCatalog,
    TreeCatalog
  },
  methods: {
    showIniJson(visualJson) {
      if (visualJson['catalog'] !== undefined) {}

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
