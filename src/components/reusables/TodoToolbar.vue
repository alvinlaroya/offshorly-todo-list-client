<template>
  <div class="toolbar">
    <v-toolbar dense class="elevation-0">
      <v-toolbar-title>{{ title }}</v-toolbar-title>
      <v-spacer></v-spacer>
      <slot name="actions"></slot>
    </v-toolbar>
    <v-container>
      <v-row>
        <v-col cols="6">
          <span class="ml-1 red--text">Remaining: {{ remaining }}</span
          ><br />
          <span class="ml-1 green--text">Completed: {{ completed }}</span>
        </v-col>
        <v-col cols="6" class="text-right">
          <v-progress-circular
            :value="progress"
            color="success"
            size="40"
            width="6"
          ></v-progress-circular>
        </v-col>
      </v-row>
    </v-container>
    <v-divider></v-divider>
  </div>
</template>

<script>
// @ is an alias to /src

export default {
  name: "Home",
  components: {},
  props: {
    title: {
      type: String,
      default: "Title",
    },
    remaining: {
      type: Number,
    },
    completed: {
      type: Number,
    },
    progress: {
      type: Number,
    },
  },
};
</script>
