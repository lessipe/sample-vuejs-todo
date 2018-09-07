<template>
  <div class="container">
    <div class="col-md-6 offset-md-3">
      <h1 class="text-center mt-5 mb-4">To-Do App</h1>
      <input type="text" class="form-control form-control-lg mb-4" v-model="newTodo" @keyup.enter="addNewTodo">

      <div class="list-group mb-4">
        <Todo
          v-for="todo in currentTodoList"
          :title="todo.title"
          :status="todo.status"
          @toggleStatus="toggleTodoStatus(todo)"
        />
      </div>

      <div class="text-right">
        <button type="button" class="btn btn-sm" :class="{'btn-primary': listType === 'active', 'btn-secondary': listType !== 'active'}" @click="changeListType('active')">
          할일
        </button>
        <button type="button" class="btn btn-sm" :class="{'btn-primary': listType === 'done', 'btn-secondary': listType !== 'done'}" @click="changeListType('done')">
          완료
        </button>
        <button type="button" class="btn btn-sm" :class="{'btn-primary': listType === 'all', 'btn-secondary': listType !== 'all'}" @click="changeListType('all')">
          전체
        </button>
      </div>
    </div>
  </div>
</template>

<script>
import Todo from './components/Todo';

export default {
  data() {
    return {
      newTodo: '',
      todoList: [],
      listType: 'active'
    };
  },
  computed: {
    currentTodoList() {
      return this.todoList.filter(todo => this.listType === 'all' || todo.status === this.listType);
    }
  },
  methods: {
    addNewTodo() {
      if (this.newTodo.trim() === '') {
        alert('할 일을 적어주세요.');
        return;
      }

      this.todoList.push({
        title: this.newTodo,
        status: 'active'
      });

      this.newTodo = '';
    },
    toggleTodoStatus(todo) {
      todo.status = todo.status === 'done' ? 'active' : 'done';
    },
    changeListType(type) {
      this.listType = type;
    }
  },
  components: {
    Todo
  }
}
</script>
