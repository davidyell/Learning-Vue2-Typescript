<template>
  <div id="task" @click="toggleComplete()">
    <p>
      {{ taskName }}
      <span v-if="isComplete" :class="{ complete: isComplete }">&check;</span>
      <span v-else>&cross;</span>
    </p>
  </div>
</template>

<script lang="ts">
import { Component, Prop, Emit, Vue } from 'vue-property-decorator'
import ToggleTaskEventPayload from './ToggleTaskEventPayloadInterface'

/**
 * Create a Vue class component using the decorators
 *
 * @see https://vuejs.org/v2/guide/typescript.html#Class-Style-Vue-Components
 * @see https://github.com/kaorun343/vue-property-decorator#Prop
 */
@Component
export default class Task extends Vue {
  @Prop(String) taskName!: string
  @Prop(Boolean) isComplete!: boolean
  @Prop(Number) index!: number

  @Emit()
  toggleComplete (): ToggleTaskEventPayload {
    return {
      targetState: !this.isComplete,
      index: this.index
    }
  }
}
</script>
