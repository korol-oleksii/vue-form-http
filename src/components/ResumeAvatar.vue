<template>
  <div class="resume-avatar" :key="resumeData.avatar">
    <div class="avatar" v-if="resumeData.avatar">
      <img :src="resumeData.avatar" class="fit-cover" alt="">
    </div>
  </div>
</template>

<script>
export default {
  props: ['resumeData']
}
</script>

<style scoped>
  .avatar {
    width: 120px;
    height: 120px;
    border-radius: 50%;
    overflow: hidden;
    margin-right: 32px;
  }
</style>
