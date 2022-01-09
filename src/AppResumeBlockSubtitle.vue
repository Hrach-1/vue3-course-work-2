<template>
  <h2>{{ content }}</h2>
</template>

<script>
export default {
  name: 'AppResumeBlockSubtitle',
  props: {
    content: {
      type: String,
      required: true
    }
  }
}
</script>
