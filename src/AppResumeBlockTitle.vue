<template>
  <h1>{{ content }}</h1>
</template>

<script>
export default {
  name: 'AppResumeBlockTitle',
  props: {
    content: {
      type: String,
      required: true
    }
  }
}
</script>
