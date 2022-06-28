<template>
  <div class="text-center">
    <v-dialog v-model="dialog" width="500" persistent>
      <v-card>
        <v-card-title class="text-h5 grey lighten-2"> Add Todo </v-card-title>

        <v-card-text>
          <v-form ref="form" v-model="valid" lazy-validation>
            <v-text-field
              v-model="task.title"
              :counter="10"
              :rules="titleRules"
              label="Title"
              required
            ></v-text-field>

            <v-text-field
              v-model="task.desc"
              :rules="descRules"
              label="Description"
              required
            ></v-text-field>

            <v-menu
              ref="menu"
              v-model="menu"
              :close-on-content-click="false"
              :return-value.sync="task.dueDate"
              transition="scale-transition"
              offset-y
              min-width="auto"
            >
              <template v-slot:activator="{ on, attrs }">
                <v-text-field
                  v-model="task.dueDate"
                  label="Due Date"
                  prepend-icon="mdi-calendar"
                  v-bind="attrs"
                  v-on="on"
                ></v-text-field>
              </template>
              <v-date-picker v-model="task.dueDate" no-title scrollable>
                <v-spacer></v-spacer>
                <v-btn text color="primary" @click="menu = false">
                  Cancel
                </v-btn>
                <v-btn
                  text
                  color="primary"
                  @click="$refs.menu.save(task.dueDate)"
                >
                  OK
                </v-btn>
              </v-date-picker>
            </v-menu>
          </v-form>
        </v-card-text>

        <v-divider></v-divider>

        <v-card-actions>
          <v-spacer></v-spacer>
          <v-btn color="error" @click="closeDialogHandler"> Close </v-btn>
          <v-btn
            :disabled="!valid"
            color="success"
            class="mr-1"
            @click="validate"
          >
            Save Task
          </v-btn>
        </v-card-actions>
      </v-card>
    </v-dialog>
  </div>
</template>
<script>
export default {
  props: {
    dialog: {
      type: Boolean,
      default: false,
    },
  },
  data() {
    return {
      valid: true,
      task: {
        title: "",
        desc: "",
        dueDate: "",
      },
      titleRules: [(v) => !!v || "Required"],
      descRules: [
        (v) => !!v || "Required",
        (v) =>
          (v && v.length >= 10) || "Title must be greater than 10 characters",
      ],
      menu: null,
      select: null,
      items: ["Item 1", "Item 2", "Item 3", "Item 4"],
      checkbox: false,
    };
  },
  methods: {
    validate() {
      this.$refs.form.validate();
    },
    reset() {
      this.$refs.form.reset();
    },
    resetValidation() {
      this.$refs.form.resetValidation();
    },
    closeDialogHandler() {
      this.$emit("update:dialog", false);
    },
  },
};
</script>
