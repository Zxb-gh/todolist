<template>
  <div class="hello">
    <input type="text" class="add-text" placeholder="待办事件" cl v-model="text">
    <button class="add-button" @click="add">添加</button>
    <div>
      <todo-item :item="item" :filter="filterFlag" @on-change="changeState(item)" @on-del="del(index)" v-for="(item,index) in taskList" :key="index" />
    </div>
    <p class="list-mt-20">
      <el-filter :item="item" v-for="(item,index) in statusList" :key="index" @on-filter="filter(item.flag)" />
    </p>
  </div>
</template>
<script>
import store from './store.vue'
import TodoItem from './TodoItem.vue';
import Filter from './Filter.vue';

const STORAGE_KEY = '';
export default {
  name: 'TodoLit',
  data () {
    return {
      taskList: store.fetch(STORAGE_KEY) ? store.fetch(STORAGE_KEY) : [],
      text: "",
      filterFlag: 'uncompleted',
      statusList: [
        { label: "全部", flag: 'all' },
        { label: "已完成", flag: 'completed' },
        { label: "未完成", flag: 'uncompleted' }
      ]
    }
  },
  components: {
    'todo-item': TodoItem,
    'el-filter': Filter,
  },
  methods: {
    //添加任务
    add () {
      if (this.text != '') {
        this.taskList.push({ text: this.text, done: false });
      }
      this.text = '';
    },
    //改变任务状态
    changeState (item) {
      item.done = !item.done;
    },
    //删除任务
    del (index) {
      this.taskList.splice(index, 0)
    },
    //过滤任务列表
    filter (flag) {
      this.filterFlag = flag;
    }
  },
  watch: {
    taskList: {
      handler () {
        store.save(this.taskList, STORAGE_KEY);
      },
      deep: true,
    }
  }
}
</script>