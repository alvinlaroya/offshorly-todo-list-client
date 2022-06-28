<template>
  <div>
    <v-card max-width="700" class="mx-auto" tile>
      <TodoToolbar
        title="Todos"
        :remaining="remainingTasks"
        :completed="completedTasks"
        :progress="progress"
      >
        <template #actions>
          <v-btn tile color="success">
            <v-icon left> mdi-plus </v-icon>
            Add Todo
          </v-btn>
        </template>
      </TodoToolbar>
      <v-card-text style="max-height: 75vh; overflow: auto" class="pa-0">
        <v-list two-line dense>
          <template v-for="(item, index) in tasks">
            <v-list-item :key="index" dense>
              <v-list-item-action>
                <v-checkbox
                  :input-value="item.done"
                  v-model="item.done"
                  :color="item.done ? 'success' : 'primary'"
                ></v-checkbox>
              </v-list-item-action>
              <v-list-item-content
                :style="{
                  color: item.done ? '#27cc63' : 'black',
                }"
                :class="[{ 'text-decoration-line-through': item.done }]"
              >
                <v-list-item-title
                  v-html="item.title"
                  :class="[{ 'green--text': item.done }]"
                ></v-list-item-title>
                <v-list-item-subtitle
                  v-text="item.subtitle"
                  :class="[{ 'green--text': item.done }]"
                ></v-list-item-subtitle>
              </v-list-item-content>
              <v-list-item-action>
                <v-scroll-x-transition>
                  <v-list-item-action-text
                    v-if="!item.done"
                    class="mr-4"
                    :class="[
                      { 'green--text': item.done },
                      { 'text-decoration-line-through': item.done },
                    ]"
                    >{{ item.dueDate }}</v-list-item-action-text
                  >
                </v-scroll-x-transition>
                <v-menu
                  transition="slide-y-transition"
                  bottom
                  offset-y
                  min-width="150"
                >
                  <template v-slot:activator="{ on, attrs }">
                    <v-btn icon v-bind="attrs" v-on="on" @click="alet(1)">
                      <v-icon>mdi-dots-vertical</v-icon>
                    </v-btn>
                  </template>
                  <v-list>
                    <v-list-item>
                      <v-icon class="mr-3">mdi-eye-outline</v-icon>
                      <v-list-item-title>View</v-list-item-title>
                    </v-list-item>
                    <v-list-item>
                      <v-icon class="mr-3">mdi-pencil-outline</v-icon>
                      <v-list-item-title>Edit</v-list-item-title>
                    </v-list-item>
                    <v-list-item>
                      <v-icon class="mr-3">mdi-delete-outline</v-icon>
                      <v-list-item-title>Delete</v-list-item-title>
                    </v-list-item>
                  </v-list>
                </v-menu>
              </v-list-item-action>
            </v-list-item>
            <v-divider
              v-if="index < tasks.length - 1"
              :key="index + 'divider'"
            ></v-divider>
          </template>
        </v-list>
      </v-card-text>
    </v-card>
    <add-todo-dialog :dialog.sync="addDialog"></add-todo-dialog>
  </div>
</template>

<script>
import TodoToolbar from "./TodoToolbar.vue";
const AddTodoDialog = () => import("@/components/dialogs/AddTodoDialog.vue");
export default {
  components: {
    TodoToolbar,
    AddTodoDialog,
  },
  data: () => ({
    checkbox: false,
    addDialog: true,
    tasks: [
      {
        avatar: "https://cdn.vuetifyjs.com/images/lists/2.jpg",
        title: 'Summer BBQ <span class="grey--text text--lighten-1">4</span>',
        dueDate: "8:00 am June 24, 2022",
        subtitle: `to Alex, Scott, Jennifer</span> &mdash; Wish I could come, but I'm out of town this  a wf afa aw fawf awf awf awf awf awawf wweekend.`,
        done: true,
      },
      {
        avatar: "https://cdn.vuetifyjs.com/images/lists/3.jpg",
        title: "Oui oui",
        dueDate: "10:00 am March 24, 2022",
        subtitle:
          "Sandra Adams</span> &mdash; Do you have Paris recommendations? Have you ever been?",
        done: true,
      },
      {
        avatar: "https://cdn.vuetifyjs.com/images/lists/4.jpg",
        title: "Birthday gift",
        dueDate: "9:00 am April 24, 2022",
        subtitle:
          "Trevor Hansen</span> &mdash; Have any ideas about what we should get Heidi for her birthday?",
        done: false,
      },
      {
        avatar: "https://cdn.vuetifyjs.com/images/lists/5.jpg",
        title: "Recipe to try",
        dueDate: "8:00 am June 24, 2022",
        subtitle:
          "Britta Holt</span> &mdash; We should eat this: Grate, Squash, Corn, and tomatillo Tacos.",
        done: false,
      },
      {
        avatar: "https://cdn.vuetifyjs.com/images/lists/2.jpg",
        title: 'Summer BBQ <span class="grey--text text--lighten-1">4</span>',
        dueDate: "8:00 am June 24, 2022",
        subtitle: `to Alex, Scott, Jennifer</span> &mdash; Wish I could come, but I'm out of town this  a wf afa aw fawf awf awf awf awf awawf wweekend.`,
        done: true,
      },
      {
        avatar: "https://cdn.vuetifyjs.com/images/lists/3.jpg",
        title: "Oui oui",
        dueDate: "10:00 am March 24, 2022",
        subtitle:
          "Sandra Adams</span> &mdash; Do you have Paris recommendations? Have you ever been?",
        done: true,
      },
    ],
  }),
  computed: {
    completedTasks() {
      return this.tasks.filter((task) => task.done).length;
    },
    progress() {
      return (this.completedTasks / this.tasks.length) * 100;
    },
    remainingTasks() {
      return this.tasks.length - this.completedTasks;
    },
  },
};
</script>
