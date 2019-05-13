<template>
  <div id="app">
    <header>
      <h1>{{title}}</h1>
    </header>

    <MarkdownEditor />
  </div>
</template>

<script>
import MarkdownEditor from "@/components/MarkdownEditor";

export default {
  name: 'app',
  components: {
    MarkdownEditor
  },

  computed: {
    title() {
      return location.pathname;
    }
  }
}
</script>

<style>
html, body {
  margin: 0;
  padding: 0;

  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}
</style>
