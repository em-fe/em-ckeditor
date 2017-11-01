<template>
  <div>
    这是刚开始的数据: {{ data1 }}
    <br>
    <br>
    <button @click="get">获取内容</button>
    <br>
    <br>
    <div v-show="subData">提交内容为：{{subData}}</div>
    <br>
    <br>
    <em-ckeditor v-model="data1" :className="{'editor-page': true}"></em-ckeditor>
    <br>
    <h3>API</h3>
    <table>
      <thead>
        <tr>
          <th>属性</th>
          <th>说明</th>
          <th>类型</th>
          <th>默认值</th>
        </tr>
      </thead>
      <tbody>
        <tr>
          <td>change</td>
          <td>改变内容触发</td>
          <td>Function</td>
          <td>-</td>
        </tr>
        <tr>
          <td>text</td>
          <td>默认内容</td>
          <td>String</td>
          <td>-</td>
        </tr>
        <tr>
          <td>className</td>
          <td>自定义的 class 名称。</td>
          <td>Object</td>
          <td>-</td>
        </tr>
        <tr>
          <td>id</td>
          <td>编辑器的 id</td>
          <td>String</td>
          <td>emeditor</td>
        </tr>
        <tr>
          <td>height</td>
          <td>编辑器的 height</td>
          <td>Number</td>
          <td>200</td>
        </tr>
      </tbody>
    </table>
    <br>
    <h3>注册的方法</h3>
    <table>
      <thead>
        <tr>
          <th>事件名</th>
          <th>说明</th>
          <th>返回值</th>
        </tr>
      </thead>
      <tbody>
        <tr>
          <td>change</td>
          <td>改变触发的方法</td>
          <td>val</td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
export default {
  data() {
    return {
      data1: '<p>test</p>',
      subData: '',
    };
  },
  methods: {
    get() {
      var editorElement = window.CKEDITOR.document.getById('editor');
      var data = window.CKEDITOR.instances.emeditor.getData();
      this.subData = data;
    },
  },
}
</script>

<style>
.editor-page {
  width: 60%;
  margin: 0 auto;
}
</style>
