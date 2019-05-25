<!-- 
 Author: jamcha <https://github.com/jamcha-aa/Annin>
 Original author of "save" function is fukami (https://codepen.io/fffkm/pen/NLxbYV)
 (c) 2018 fukami, (c) 2019 jamcha.
 License: MIT License
-->

<template>
  <div id="app">
    <div id="cc">
    <p> {{ value.length }} / {{ value.trim().split(/\s+/).length }} </p>
    </div>
    <div id="fr">
    <text-reader @load="value = $event"></text-reader>
    </div>
    <div id="editor">
    <mavon-editor style="height: 100%" @save="save" v-model="value" language="en" :toolbars="toolbars" placeholder="編集を始てね！" defaultOpen="edit" :subfield=false />
    </div>
  </div>
</template>

<script>
import moment from 'moment';
import TextReader from "./TextReader";
export default {
  name: 'Annin',
  data() {
    return {
      value: '',
      toolbars: {
      bold: false, // 粗体
      italic: false, // 斜体
      header: false, // 标题
      underline: false, // 下划线
      strikethrough: false, // 中划线
      mark: false, // 标记
      superscript: false, // 上角标
      subscript: false, // 下角标
      quote: false, // 引用
      ol: false, // 有序列表
      ul: false, // 无序列表
      link: false, // 链接
      imagelink: false, // 图片链接
      code: false, // code
      table: false, // 表格
      fullscreen: false, // 全屏编辑
      readmodel: true, // 沉浸式阅读
      htmlcode: false, // 展示html源码
      help: false, // 帮助
      /* 1.3.5 */
      undo: false, // 上一步
      redo: false, // 下一步
      trash: false, // 清空
      save: true, // 保存（触发events中的save事件）
      /* 1.4.2 */
      navigation: false, // 导航目录
      /* 2.1.8 */
      alignleft: false, // 左对齐
      aligncenter: false, // 居中
      alignright: false, // 右对齐
      /* 2.2.1 */
      subfield: true, // 单双栏模式
      preview: false, // 预览
      }
    }
  },
  methods: {
    save: function () {
      var blob = new Blob([ this.value ], {'type': 'text/plain'});
      let link = document.createElement('a');
      link.href = window.URL.createObjectURL(blob);
      link.download = moment(new Date).format('YYYY-MM-DD ddd HH-mm-ss') + '.md';
      link.click();
      window.URL.revokeObjectURL(link);
    }
  },
  components: {
    TextReader
  }
}
</script>
  
<style>
#editor {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin: auto;
  margin-top: 80px;
  width: 740px;
  height: 500px;
}
#fr {
  position: absolute;
  top: 50px;
  right: 10px;
  color: #b3b3b3;
}
#cc {
  position: absolute;
  top: 0px;
  right: 10px;
  color: #b3b3b3;
}
</style>

