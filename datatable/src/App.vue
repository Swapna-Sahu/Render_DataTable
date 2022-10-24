<template>
  <div id="app">
    <ItemList />
  </div>
</template>

<script>

import ItemList from "./components/ItemList";
export default {
  name: "App",
  components: {
    ItemList,
  },
};
</script>

<style>
body {
  font-family:  sans-serif;
  background-color: black;
  color: azure;
  margin: 100px;
  margin-top: 10%;
}
</style>