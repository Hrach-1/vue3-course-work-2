<template>
  <div class="container column">
    <app-resume-form
      @add-block="saveResumeBlock"
    ></app-resume-form>
    <app-resume-structure
      :blocks="resumeBlocks"
    ></app-resume-structure>
  </div>

  <div class="container">
    <app-loader
      v-if="loadingComments"
    ></app-loader>
    <p v-else-if="!loadingComments && comments.length === 0">
      <button class="btn primary" @click="loadComments">Загрузить комментарии</button>
    </p>

    <app-comment-list
      v-if="comments.length > 0"
      :comments="comments"
    ></app-comment-list>
  </div>
</template>

<script>
import AppResumeForm from '@/AppResumeForm'
import AppResumeStructure from '@/AppResumeStructure'
import AppCommentList from '@/AppCommentList'
import AppLoader from '@/AppLoader'

export default {
  data () {
    return {
      resumeBlocks: [],
      blockTypes: {
        title: 'app-resume-block-title',
        subtitle: 'app-resume-block-subtitle',
        text: 'app-resume-block-text',
        avatar: 'app-resume-block-avatar'
      },

      comments: [],
      loadingComments: false,

      serverUrl: 'https://vue3-course-work-2-246a0-default-rtdb.firebaseio.com/'
    }
  },
  async mounted () {
    await this.loadResume()
  },
  methods: {
    async loadComments () {
      try {
        this.loadingComments = true
        const url = 'https://jsonplaceholder.typicode.com/comments?_limit=42'
        const response = await fetch(url, {
          method: 'GET',
          headers: {
            'Content-Type': 'application/json'
          }
        })
        this.comments = await response.json()
        this.loadingComments = false
      } catch (e) {
        console.warn('loadComments : ', e.message)
      }
    },

    async saveResumeBlock (type, content) {
      try {
        const component = this.blockTypes[type]

        if (component) {
          const response = await fetch(this.serverUrl + 'resume.json', {
            method: 'POST',
            headers: {
              'Content-Type': 'application/json'
            },
            body: JSON.stringify({
              type,
              content
            })
          })

          this.resumeBlocks.push({
            id: response.name,
            component,
            content
          })
        }
      } catch (e) {
        console.warn('saveResumeBlock : ', e.message)
      }
    },

    async loadResume () {
      try {
        const response = await fetch(this.serverUrl + 'resume.json', {
          method: 'GET',
          headers: {
            'Content-Type': 'application/json'
          }
        })
        const data = await response.json()

        this.resumeBlocks = Object.keys(data).map(key => {
          const component = this.blockTypes[data[key].type]
          return {
            id: key,
            content: data[key].content,
            component
          }
        })
      } catch (e) {
        console.warn('loadResume : ', e.message())
      }
    }
  },
  components: {
    AppLoader,
    AppCommentList,
    AppResumeStructure,
    AppResumeForm
  }
}
</script>

<style>
.avatar {
  display: flex;
  justify-content: center;
}

.avatar img {
  width: 150px;
  height: auto;
  border-radius: 50%;
}
</style>
