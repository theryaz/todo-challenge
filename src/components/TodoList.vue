<template>
  <v-container>
    <v-row class="text-center">
      <v-col cols="6" offset="3">
        <v-form @submit.prevent="addTodo(newText)" class="d-flex">
          <v-text-field
            outlined
            v-model="newText"
            label="Add a new task"
            hide-details
          />
          <v-btn class="my-auto ml-4" :disabled="!newText || newText.length === 0" @click="addTodo(newText)">
            Add
          </v-btn>
          <button type="submit" hidden />
        </v-form>
      </v-col>
    </v-row>
    <v-row>
      <v-col cols="6" offset="3">
        <v-list>
          <v-slide-y-transition group>
            <v-list-item v-for="(item, index) of todoList" :key="index">
              <v-list-item-icon>
                <v-checkbox
                  color="secondary"
                  @change="item.toggleDone()"
                  :value="item.done"
                />
              </v-list-item-icon>
              <v-list-item-content @click="item.toggleDone()">
                {{ item.name }}
              </v-list-item-content>
              <v-btn @click="deleteItem(index)" icon>
                <v-icon>
                  mdi-trash-can-outline
                </v-icon>
              </v-btn>
            </v-list-item>
          </v-slide-y-transition>
        </v-list>
      </v-col>
    </v-row>
  </v-container>
</template>

<script lang="ts">
import { Component, Vue } from 'vue-property-decorator';

class TodoItem{
  done = false;
  created: Date;
  constructor(public name: string){
    this.created = new Date();
  }
  toggleDone(){
    this.done = !this.done;
  }
}

@Component
export default class TodoList extends Vue{
  newText = "";
  todoList: TodoItem[] = [
    new TodoItem("Make a todo list"),
    new TodoItem("Pickup milk"),
  ];

  addTodo(name: string){
    this.todoList.push(new TodoItem(name));
    this.newText = "";
  }
  deleteItem(index: number){
    this.todoList.splice(index, 1);
  }
}
</script>
