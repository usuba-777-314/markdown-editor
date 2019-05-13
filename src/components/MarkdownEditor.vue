<template>
  <div class="markdown-editor">
    <textarea class="editor" v-model="text"></textarea>
    <div class="viewer" v-html="markup"></div>
  </div>
</template>

<script>
import marked from "marked";

export default {
  data() {
    return {
      text: `[Google](https://www.google.com/)はこちら

[Yahoo! Japan](http://yahoo.co.jp)はこちら

[Twitter](https://twitter.com/i/notifications?lang=ja)はこちら

[Editor1](/editor1)はこちら

[Editor2](${location.origin}/editor2)はこちら`
    };
  },

  computed: {
    markup() {
      let markup = marked(this.text, { sanitize: true });

      markup = markup.replace(/href="(.+)"/g, (match, href) => {
        if (href[0] === "/") return match;
        if (href.indexOf(location.origin) === 0) return match;

        return match + ` target="_blank"`;
      });

      return markup;
    }
  }
};
</script>

<style scoped>
.markdown-editor {
  width: 100vw;
  height: 100vh;

  display: flex;
}

.editor, .viewer {
  flex-basis: 50%;
  height: 100%;
  min-height: 100%;
  max-height: 100%;

  padding: 8px;
  font-size: 14px;

  border: 1px solid rgba(153, 153, 153, 0.2);
}
</style>
