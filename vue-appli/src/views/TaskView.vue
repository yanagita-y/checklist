<template>
  <div class="task">
    <h1>{{ projectName }}</h1>
    <p>このプログラムは、<a href="https://he-tree-vue.phphe.com/guide.html" target="_blank">he-tree-vue</a>のサンプルです。</p>
    <p><a href="https://he-tree-vue.phphe.com/guide.html#check-plugin" target="_blank">check-plugin</a>の手順通りに実装したところ、slot-scopeでエラーが発生したので、そこを解消させています。</p>
    <p>チェックボックスクリック時→通常のチェックtoggle、テキストクリック時→モーダル表示となるように、処理を追加してください。</p>
    <Tree :value="treeData">
      <template v-slot="{ node, index, path }">
        <b>{{ index }}</b>
        <small>{{ path }}</small>
        <input type="checkbox" @change="toggleStatus(node.taskID, node.text)">
        <a href="#" @click="showChangeStatusModal(node.taskID, node.text)">{{node.text}}</a>
      </template>
    </Tree>
  </div>
</template>

<script>
import 'he-tree-vue/dist/he-tree-vue.css'
import {Tree, Draggable, Check} from 'he-tree-vue'
export default {
  components: {Tree: Tree.mixPlugins([Draggable, Check])},
    data() {
      return{
        projectName : "ここに案件名が入ります",
        treeData: [
          {text: 'node 1', taskID: 1},
          {text: 'node 2', taskID:2,
            children: [
              {text: 'node 2-1', taskID:3},
              {text: 'node 2-2', taskID:4,
                children: [
                  {text: 'node 2-2-1', taskID:5},
                  {text: 'node 2-2-2', taskID:6},
                ]
              },
              {text: 'node 2-3', taskID:7},
              {text: 'node 2-4', taskID:8},
            ]
          },
        ]
      }
    },
    methods:{
      toggleStatus(taskID, taskName){
        alert('[taskID:' + taskID + ']' + taskName + 'のステータスをDBに書き込む処理をここに書く');
      },
      showChangeStatusModal(taskID, taskName){
        alert('[taskID:' + taskID + ']' + taskName + 'のステータスを変更するモーダルを表示する処理をここに書く');
      },
    },
}
</script>
    