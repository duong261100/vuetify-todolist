<template>
  <v-dialog
    v-model="showDialog"
    scrollable
    :overlay="false"
    max-width="290px"
    transition="dialog-transition"
  >
    <template v-slot:activator="{ on }">
      <v-btn icon v-on="on">
        <v-icon>mdi-plus</v-icon>
      </v-btn>
    </template>
    <v-card>
      <v-card-title class="headline teal--text"> Create New Task </v-card-title>
      <v-card-text>
        <v-form ref="form">
          <v-text-field
            v-model="form.title"
            name="title"
            label="title"
            required
            :rules="rules.title"
          ></v-text-field>
          <v-text-field
            v-model="form.description"
            name="description"
            label="description"
            required
            :rules="rules.description"
          ></v-text-field>
        </v-form>
      </v-card-text>
      <v-card-actions>
        <v-spacer></v-spacer>
        <v-btn color="teal" text @click="saveTask">Save</v-btn>
      </v-card-actions>
    </v-card>
  </v-dialog>
</template>

<script>
export default {
  data() {
    return {
      showDialog: false,
      form: {
        title: null,
        description: null,
      },
      rules: {
        title: [
          (v) => !!v || "Title is required",
          (v) =>
            (!!v && v.length > 2) || "Title must be longer than 2 characters",
        ],
        description: [
          (v) => !!v || "Description is required",
          (v) =>
            (!!v && v.length <= 50) ||
            "Description must be shorter than 50 characters",
        ],
      },
    };
  },
  methods: {
    saveTask() {
      if (this.$refs.form.validate()) {
        this.$store.dispatch( 'task/add', this.form )
        this.$refs.form.reset()
        this.showDialog = false
      }
    },
  }
};
</script>

<style>
</style>