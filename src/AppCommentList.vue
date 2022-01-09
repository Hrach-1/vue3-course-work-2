<template>
  <div>
    <div class="card" v-if="comments.length">
      <h2>Комментарии</h2>
      <ul class="list">
        <li
          class="list-item"
          v-for="comment in comments"
          :key="comment.id"
        >
          <app-comment-card
            :email="comment.email"
            :body="comment.body"
          ></app-comment-card>
        </li>
      </ul>
    </div>
  </div>

</template>

<script>
import AppCommentCard from '@/AppCommentCard'

export default {
  name: 'AppCommentList',
  props: {
    comments: {
      type: Array,
      required: true
    }
  },
  components: { AppCommentCard }
}
</script>
