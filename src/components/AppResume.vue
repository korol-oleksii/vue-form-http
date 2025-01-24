<template>

  <div class="card card-auto" v-if="resumeData.id">
    <div class="card__body">
      <div class="card__columns card-v-center">
        <div class="card__column">
          <resume-avatar :resumeData="resumeData"></resume-avatar>
        </div>
        <div class="card__column">
          <resume-title :resumeData="resumeData"></resume-title>
        </div>
      </div>
      <div class="content">
        <resume-content :resumeData="resumeData"></resume-content>
      </div>
    </div>
  </div>

  <div class="card card-auto" v-else>
    <h3>Додайте перший блок, щоб побачити результат</h3>
  </div>

</template>

<script>
import ResumeTitle from '@/components/ResumeTitle.vue'
import ResumeAvatar from '@/components/ResumeAvatar.vue'
import ResumeContent from '@/components/ResumeContent.vue'

export default {
  inject: ['resumeData'],
  components: {ResumeTitle, ResumeAvatar, ResumeContent},
}
</script>

<style lang="scss" scoped>
  .card {
    p {
      font-size: 16px;
      line-height: 20px;
    }
  }
</style>
