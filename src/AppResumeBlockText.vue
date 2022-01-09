<template>
  <p>{{ content }}</p>
</template>

<script>
export default {
  name: 'AppResumeBlockText',
  props: {
    content: {
      type: String,
      required: true
    }
  }
}
</script>
