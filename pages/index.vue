<template>
  <v-row justify="center" align="center">
    <v-col cols="12" sm="8" md="6">
      <v-card max-width="475" class="mx-auto">
        <v-toolbar color="teal">
          <v-app-bar-nav-icon>
            <v-icon>mdi-text-box-check</v-icon>
          </v-app-bar-nav-icon>
          <v-toolbar-title>Todo List</v-toolbar-title>
          <v-spacer />
          <add-task-button />
        </v-toolbar>

        <v-list>
          <v-subheader>In Progress Tasks</v-subheader>
          <v-list-item-group>
            <task-item v-for="(task, i) in pendingTasks" :key="i" :task="task" />
          </v-list-item-group>

          <v-subheader>Done Tasks</v-subheader>
          <v-list-item-group>
            <task-item v-for="(task, i) in doneTasks" :key="i" :task="task" />
          </v-list-item-group>
        </v-list>
      </v-card>
    </v-col>
  </v-row>
</template>

<script>
import { mapGetters } from "vuex"
export default {
  name: "IndexPage",

  computed: {
    ...mapGetters({
      doneTasks: 'task/doneTasks',
      pendingTasks: 'task/pendingTasks'
    }),
  },
};
</script>
