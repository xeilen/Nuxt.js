<template>
  <h1>Event #{{ event.title }}</h1>
</template>

<script>
export default {
  name: 'Id',
  // props: {
  //   event: {
  //     type: Object,
  //     default: null,
  //   },
  // },
  async asyncData({ $axios, error, params }) {
    try {
      const response = await $axios.get(
        'http://localhost:3000/events/' + params.id
      )
      return {
        event: response.data,
      }
    } catch (e) {
      error({
        statusCode: 503,
        message: 'Unable to fetch event #' + params.id,
      })
    }
  },
  head() {
    return {
      title: 'Event #' + this.event.title,
      meta: [
        {
          hid: 'description',
          name: 'description',
          content: 'What you need to know about event #' + this.event.title,
        },
      ],
    }
  },
}
</script>

<style scoped></style>
