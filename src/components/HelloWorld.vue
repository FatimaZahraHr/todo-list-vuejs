<template>
  <v-container>
     <v-card elevation="4" class="mx-auto mt-4 pa-4">
          <h1>Todo list</h1>
          <v-text-field v-model="newItem" type="text" placeholder="New task" color="grey" @keyup.enter="addItem">
            <v-btn slot="append" icon tile color="red" elevation="0" @click="addItem">
              <v-icon color="black">mdi-plus</v-icon>
            </v-btn>   
          </v-text-field>

          <div v-if="items.length > 0" class="pt-4">
            <v-btn class="mx-auto white--text" color="green" elevation="0" medium outlined @click="clearCompleted">
              <v-icon>mdi-delete</v-icon>Delete completed tasks
            </v-btn>
            <v-btn class="mx-auto white--text" color="orange" elevation="0" medium outlined @click="clearItems">
              <v-icon>mdi-delete</v-icon>Delete all
            </v-btn>
          </div>

          <div v-if="items.length > 0" class="pt-4">
            <ul class="pl-4">
              <li v-for="(item, index) in items" :key="`item-${index}`" class="tasks-list">
                <div class="d-flex justify-space-between align-center">

                  <p class="py-2 px-0" :class="{ 'item-done': item.completed }">
                    {{ item.title }}
                  </p>
                  <div class="py-2 px-0">
                    <v-btn xsmall icon tile color="" elevation="0" @click="removeItem(index)">
                      <v-icon color="red">mdi-close</v-icon>
                    </v-btn>

                    <v-btn xsmall icon tile color="" elevation="0" @click="completeItem(item)">
                      <v-icon color="green">mdi-check</v-icon>
                    </v-btn>
                  </div>

                </div>
              </li>
            </ul>
          </div>
          <div v-else class="pa-4">
            <div class="grey--text text--lighten-1 d-flex justify-center">No tasks yet!</div>
          </div>
        </v-card>
  </v-container>
</template>

<script>
  export default {
    name: 'HelloWorld',
  data: () => ({
    newItem: "",
    items: []
  }),
  computed: {
    incomplete() {
      return this.items.filter();
    }
  },
  methods: {
    addItem() {
      if (this.newItem) {
        this.items.push({
          title: this.newItem,
          completed: false
        });
        this.newItem = "";
      }
    },
    removeItem(index) {
      this.items.splice(index, 1);
    },
    completeItem(item) {
      item.completed = !item.completed;
    },
    clearItems() {
      this.items = [];
    },
    clearCompleted() {
      this.items = this.items.filter(this.inProgress);
    },
    inProgress(item) {
      return !this.isCompleted(item);
    },
    isCompleted(item) {
      return item.completed;
    }
  }
  }
</script>
<style>
.item-done {
  text-decoration: line-through;
}
</style>