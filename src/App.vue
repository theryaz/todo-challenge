<template>
  <v-app>
    <v-main>
      <TodoList msg="TODO: Create a todo list"/>
    </v-main>
  </v-app>
</template>

<script lang="ts">
import Vue from 'vue';
import TodoList from './components/TodoList.vue';

export default Vue.extend({
  name: 'App',

  components: {
    TodoList,
  },

  data: () => ({
    //
  }),
});
</script>
