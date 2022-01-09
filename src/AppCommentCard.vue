<template>
  <div>
    <p><strong>{{ email }}</strong></p>
    <small>{{ body }}</small>
  </div>
</template>

<script>
export default {
  name: 'AppCommentCard',
  props: {
    email: {
      type: String,
      required: true
    },
    body: {
      type: String,
      required: true
    }
  }
}
</script>
