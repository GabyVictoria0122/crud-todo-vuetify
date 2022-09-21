<template>
  <v-main>
    <v-container>
      <v-row justify="center" class="text-center">
        <v-col cols="12">
          <h2 class="display-2 font-weight-bold mb-3">Summary Panel</h2>
        </v-col>

        <div v-for="item in data" :key="item.group">
          <v-col class="d-flex justify-space-around">
            <h3>
              {{ item.group }} <v-chip class="ma-2"> {{ item.tasks }} </v-chip>
            </h3>
          </v-col>
          <v-col class="d-flex justify-space-around">
            <v-progress-circular
              :rotate="360"
              :size="100"
              :width="15"
              :value="item.percent"
              color="blue"
            >
              {{ value }}
            </v-progress-circular>
          </v-col>
        </div>
        <v-col cols="12">
          <div class="my-4">
            <v-btn rounded color="light-blue " dark :to="{ name: 'taskList' }">
              See All Tasks
            </v-btn>
          </div>
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
      summary: {},
      data: [],
    }
  },
  methods: {
    getSummary() {
      TasksApi.summary().then((data) => {
        console.log('carregando 2', data)
        this.summary = data
        for (const [key, value] of Object.entries(data)) {
          const totalTasks = value.pending + value.working + value.done
          let obj = {
            group: key,
            tasks: totalTasks,
            percent: 100 - (value.pending / totalTasks) * 100,
          }
          this.data.push(obj)
        }
      })
    },
  },
  created() {
    console.log('carregando 1')
    this.getSummary()
  },
}
</script>
