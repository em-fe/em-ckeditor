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
    config: {
      type: Object,
      default: () => {},
    },
    id: {
      type: String,
      default: 'emeditor',
    },
    change: {
      type: Function,
      default: () => {},
    },
    cdnjs: {
      type: String,
      default: 'https://unpkg.com/ckeditor@4.10.0/ckeditor.js',
    },
    cdncss: {
      type: String,
      default: 'https://unpkg.com/ckeditor@4.10.0/contents.css',
    },
  },
  mounted() {
    const head = document.getElementsByTagName('head')[0];
    const script = document.createElement('script');
    script.src = this.cdnjs;
    head.appendChild(script);
    script.onload = () => {
      this.configEditor();
      this.afterLoadScript();
    };
  },
  methods: {
    configEditor() {
      config.contentsCss.push(this.cdncss);
    },
    afterLoadScript() {
      const editorElement = window.CKEDITOR.document.getById(this.id);
      const cfg = Object.assign({}, config, this.config);
      const editor = window.CKEDITOR.replace(this.id, cfg);
      editorElement.setHtml(this.text || this.value || '');
      this.$emit('inited', editorElement, editor, window.CKEDITOR);
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
