<template>
  <v-main class="mt-4">
    <v-container>
      <v-row>
        <v-col cols="12" sm="6">
          <v-text-field
            v-model="message"
            label="Create a Task"
            outlined
            clearable
          ></v-text-field>
        </v-col>
        <v-col
          justify="center"
          class="pa-3"
          cols="12"
          v-for="task in tasks"
          :key="task.id"
        >
          <v-list-item>
            <template v-slot:default="{ active }">
              <v-list-item-action>
                <v-checkbox :input-value="active"></v-checkbox>
              </v-list-item-action>

              <v-list-item-content>
                <v-list-item-title>{{ task.title }}</v-list-item-title>
                <v-list-item-subtitle
                  >Notify me about updates to apps or games that I downloaded
                  Notify me about updates to apps or games that I
                  downloaded</v-list-item-subtitle
                >
              </v-list-item-content>
            </template>
          </v-list-item>
        </v-col>
      </v-row>
    </v-container>
  </v-main>
</template>

<script>
import TasksApi from '@/api/tasks.api.js'

export default {
  data: () => {
    return {
      tasks: [],
    }
  },
  methods: {
    getTasks() {
      TasksApi.getTasks().then((data) => {
        this.tasks = data
      })
    },
    removerTask(taskId) {
      TasksApi.removeTask(taskId).then(() => {
        this.getTasks()
      })
    },
  },
  created() {
    this.getTasks()
    console.log('ta batendo duss vezes?')
  },
}
</script>
