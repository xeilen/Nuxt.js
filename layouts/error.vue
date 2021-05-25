<template>
  <div>
    <h1>{{ message }}</h1>
    <p v-if="statusCode === 404">
      <nuxt-link to="/">Return to homepage</nuxt-link>
    </p>
  </div>
</template>

<script>
export default {
  name: 'Error',
  props: {
    error: {
      type: Object,
      default: null,
    },
  },
  head() {
    return {}
  },
  computed: {
    statusCode() {
      return (this.error && this.error.statusCode) || 500
    },
    message() {
      return this.error.message
    },
  },
}
</script>

<style scoped></style>
