<template>
  <div class="avatar">
    <img :src="content" alt="Avatar">
  </div>
</template>

<script>
export default {
  name: 'AppResumeBlockAvatar',
  props: {
    content: {
      type: String,
      required: true
    }
  }
}
</script>
