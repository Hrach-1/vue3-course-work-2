<template>
  <form class="card card-w30" @submit.prevent="addResumeBlock">
    <div class="form-control">
      <label for="type">Тип блока</label>
      <select id="type" v-model="resumeBlockType">
        <option value="title">Заголовок</option>
        <option value="subtitle">Подзаголовок</option>
        <option value="avatar">Аватар</option>
        <option value="text">Текст</option>
      </select>
    </div>

    <div class="form-control">
      <label for="value">Значение</label>
      <textarea id="value" rows="3" v-model.trim="resumeBlockContent"></textarea>
    </div>

    <button class="btn primary" :disabled="!isFormValid">Добавить</button>
  </form>
</template>

<script>
export default {
  name: 'AppResumeForm',
  emits: {
    'add-block' (type, content) {
      let isValid = true
      const blockTypes = ['title', 'subtitle', 'avatar', 'text']
      isValid = blockTypes.includes(type)
      isValid = typeof content === 'string'
      return isValid
    }
  },
  data () {
    return {
      resumeBlockType: 'title',
      resumeBlockContent: ''
    }
  },
  methods: {
    addResumeBlock () {
      if (this.isFormValid) {
        this.$emit('add-block', this.resumeBlockType, this.resumeBlockContent)
        this.resumeBlockType = 'title'
        this.resumeBlockContent = ''
      }
    }
  },
  computed: {
    isFormValid () {
      return this.resumeBlockContent.length > 3
    }
  }
}
</script>
