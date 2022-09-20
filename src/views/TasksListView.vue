<template>
  <v-main class="overflow-hidden mt-4">
    <v-container>
      <v-row>
        <v-col class="pa-3" cols="12" v-for="task in tasks" :key="task.id">
          <v-card elevation="17" shaped>
            <v-card-text>
              <div>#{{ task.date }}</div>
              <p class="ma-0 pa-0 text-h5 text--primary">{{ task.title }}</p>
              <span class="chip #f8bbd0 pink lighten-4">{{
                task.project
              }}</span>
            </v-card-text>

            <v-card-actions>
              <v-list-item class="grow">
                <v-btn
                  x-small
                  icon
                  color="grey"
                  :to="{ name: 'taskUpdate', params: { id: task.id } }"
                  ><v-icon>fas fa-pen fa-xs</v-icon></v-btn
                >
                <v-btn x-small icon color="grey" @click="removerTask(task.id)"
                  ><v-icon>far fa-trash-alt fa-xs</v-icon></v-btn
                >
              </v-list-item>
            </v-card-actions>
          </v-card>
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
  },
}
</script>
