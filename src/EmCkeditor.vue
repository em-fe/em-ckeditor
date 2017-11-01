<template>
  <div class="em-editor" :class="className">
    <textarea :id="id"></textarea>
  </div>
</template>
<script>
import config from './config';

export default {
  name: 'EmCkeditor',
  props: {
    text: String,
    value: String,
    height: {
      type: Number,
      default: 200,
    },
    className: Object,
    id: {
      type: String,
      default: 'emeditor',
    },
    change: {
      type: Function,
      default: () => {},
    },
  },
  mounted() {
    const head = document.getElementsByTagName('head')[0];
    const script = document.createElement('script');
    script.src = 'https://cdn.ckeditor.com/4.7.3/standard-all/ckeditor.js';
    head.appendChild(script);
    script.onload = () => {
      this.afterLoadScript();
    };
  },
  methods: {
    afterLoadScript() {
      const editorElement = window.CKEDITOR.document.getById(this.id);
      const editor = window.CKEDITOR.replace(this.id, config);
      editorElement.setHtml(this.text || this.value || '');
      editor.on('change', (evt) => {
        const value = evt.editor.getData();
        this.$emit('input', value);
        this.$emit('change', value);
        this.change(value);
      });
    },
  },
};
</script>
