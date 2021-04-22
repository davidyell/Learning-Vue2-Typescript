<template>
  <div id="user">
      <h4>{{ fullName }} ({{ userAge }})</h4>
  </div>
</template>

<script lang="ts">
import Vue from 'vue'

/**
 * Exporting a comonent which extends Vue rather than implements the class-api
 *
 * @see https://vuejs.org/v2/guide/typescript.html#Basic-Usage
 */
export default Vue.extend({
  props: {
    firstName: {
      type: String,
      required: true
    },
    lastName: {
      type: String,
      required: true
    }
  },
  computed: {
    fullName (): string {
      return this.firstName + ' ' + this.lastName
    },
    userAge (): number {
      return this.$store.state.userAge
    }
  }
})
</script>

<style>

</style>
