<template>
  <div>
    <div class="cards" v-if="comments.length !== 0">
      <div class="card" v-for="comment in comments" :key="comment.id">
        <div class="email"><small>{{ comment.id }}. Comment from:</small><br />{{ comment.email }}</div>
        <div class="title"><h3>{{ comment.name }}</h3></div>
        <div class="desc">{{ comment.body }}</div>
      </div>
    </div>

    <div v-else class="cards">
      <div class="card card-auto">
        <button class="button" @click="$emit('load')">Завантажити коментарі</button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  emits: ['load'],
  props: ['comments']
}
</script>

<style lang="scss" scoped>

</style>
