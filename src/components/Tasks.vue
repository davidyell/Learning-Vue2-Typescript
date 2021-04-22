<template>
  <div id="task-list">
    <h1>Task list</h1>
    <user :first-name="firstName" :last-name="lastName"></user>
      <ul class="tasks">
          <li v-for="(item, index) in list" :key="item.name" :class="['task', { complete: item.isComplete }]">
            <task :task-name="item.name" :is-complete="item.isComplete" :index="index" @toggle-complete="toggleTaskCompletion"></task>
          </li>
      </ul>
  </div>
</template>

<script lang="ts">
import { Component, Vue } from 'vue-property-decorator'
import Task from './Task.vue'
import User from './User.vue'
import ToggleTaskEventPayload from './ToggleTaskEventPayloadInterface'

@Component({
  components: {
    Task,
    User
  },
  methods: {
    toggleTaskCompletion (payload: ToggleTaskEventPayload): void {
      this.$data.list[payload.index].isComplete = payload.targetState
    }
  }
})

export default class Tasks extends Vue {
  firstName = 'David'
  lastName = 'Yell'

  data (): Record<string, unknown> {
    return {
      list: [
        {
          name: 'Buy groceries',
          isComplete: false
        },
        {
          name: 'Paint landscape',
          isComplete: true
        }
      ]
    }
  }
}
</script>

<style lang="scss">
#task-list {
  width: 50%;
  margin: 0 auto;
  border: 1px solid #ccc;
  text-align: left;
  h1, h4 {
    text-align: center;
  }
}
ul.tasks {
  padding: 0;
  margin: 0;
  li.task {
    cursor: pointer;
    padding: 10px;
    list-style: none;
    &.complete {
      color: white;
      background-color: seagreen;
    }
  }
}
</style>
