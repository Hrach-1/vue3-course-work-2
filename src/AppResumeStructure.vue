<template>
  <div class="card card-w70">
    <template v-if="blocks.length">
      <component
        v-for="block in blocks"
        :key="block.id"
        :is="block.component"
        :content="block.content"
      />
    </template>

    <h3 v-else>Добавьте первый блок, чтобы увидеть результат</h3>
  </div>
</template>

<script>
import AppResumeBlockAvatar from '@/AppResumeBlockAvatar'
import AppResumeBlockText from '@/AppResumeBlockText'
import AppResumeBlockTitle from '@/AppResumeBlockTitle'
import AppResumeBlockSubtitle from '@/AppResumeBlockSubtitle'

export default {
  name: 'AppResumeStructure',
  components: {
    AppResumeBlockAvatar,
    AppResumeBlockText,
    AppResumeBlockTitle,
    AppResumeBlockSubtitle
  },
  props: {
    blocks: {
      type: Array,
      default: () => []
    }
  }
}
</script>
