<template>
  <div class="todo">
    <a-button>新增</a-button>
    <h1>todo page -{{ defaultColor }} - {{ author }}</h1>
  </div>
  <!-- 引用ant-design-vue -->
  <a-layout>
    <a-layout-header>待办事项</a-layout-header>
    <a-layout-content>
      <a-input-search v-model:value="todo" placeholder="新增待办事项" size="large" @search="addTodo">
        <template v-slot:enterButton>
          <a-button>新增</a-button>
        </template>
      </a-input-search>
      <h2 class="title">待办事项</h2>
      <a-card :title="`${index + 1}、${item.time}`" v-for="(item, index) in todos" :key="item.id">
        <template v-slot:extra>
          <a-switch v-model:checked="item.done" @change="handleCheck(item, true)" />
        </template>
        {{ item.content }}
      </a-card>
    </a-layout-content>
  </a-layout>
</template>
<script>
import { ref, reactive, computed } from 'vue';
import store from '../store';

export default {
  setup() {
    const todo = ref('');
    const time = `${new Date().getFullYear()}-${new Date().getMonth() + 1}-${new Date().getDate()}`;
    const state = reactive({
      defaultColor: 'red1',
      author: store.state.author,
      todoList: [
        {
          id: 1,
          done: false,
          time: time,
          content: 'todo event 1',
        },
        {
          id: 2,
          done: false,
          time: time,
          content: 'todo event 2',
        },
        {
          id: 3,
          done: false,
          time: time,
          content: 'todo event 3',
        },
      ],
    });
    const todos = computed(() => {
      return state.todoList.filter(item => !item.done);
    });
    return {
      todo,
      todos,
      ...state,
    };
  },
};
</script>
