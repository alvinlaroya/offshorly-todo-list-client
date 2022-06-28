<template>
  <div class="home">
    <v-container>
      <v-row>
        <v-col cols="12">
          <todo-container></todo-container>
        </v-col>
      </v-row>
    </v-container>
  </div>
</template>

<script>
// @ is an alias to /src
import TodoContainer from "@/components/reusables/TodoContainer.vue";

export default {
  name: "Home",
  components: {
    TodoContainer,
  },
};
</script>
